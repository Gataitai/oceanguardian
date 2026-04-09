<script lang="ts">
    import { onMount } from 'svelte';
    import * as THREE from 'three';

    let container: HTMLDivElement;

    const DEBUG = false;

    onMount(() => {
        const scene = new THREE.Scene();
        const camera = new THREE.OrthographicCamera(-1, 1, 1, -1, 0, 1);

        const renderer = new THREE.WebGLRenderer({
            alpha: true,
            antialias: true
        });

        renderer.setPixelRatio(Math.min(window.devicePixelRatio, 2));
        renderer.setSize(container.clientWidth, container.clientHeight);
        renderer.setClearColor(0x000000, 0);
        container.appendChild(renderer.domElement);

        const uniforms = {
            uMouse: { value: new THREE.Vector2(0.75, 0.5) },
            uTargetMouse: { value: new THREE.Vector2(0.75, 0.5) },
            uVelocity: { value: new THREE.Vector2(0.0, 0.0) },
            uTargetVelocity: { value: new THREE.Vector2(0.0, 0.0) },
            uAspect: { value: container.clientWidth / container.clientHeight },
            uTime: { value: 0 },
            uDebug: { value: DEBUG ? 1.0 : 0.0 }
        };

        const material = new THREE.ShaderMaterial({
            uniforms,
            transparent: true,
            vertexShader: `
                varying vec2 vUv;

                void main() {
                    vUv = uv;
                    gl_Position = vec4(position.xy, 0.0, 1.0);
                }
            `,
            fragmentShader: `
                uniform vec2 uMouse;
                uniform vec2 uVelocity;
                uniform float uAspect;
                uniform float uTime;
                uniform float uDebug;

                varying vec2 vUv;

                float blob(vec2 uv, vec2 center, float time, vec2 velocity, float aspect) {
                    vec2 p = uv - center;
                    p.x *= aspect;

                    vec2 v = velocity;
                    v.x *= aspect;

                    float speed = clamp(length(v) * 35.0, 0.0, 1.0);

                    vec2 dir = normalize(v + vec2(0.000001, 0.0));
                    vec2 sideDir = vec2(-dir.y, dir.x);

                    float along = dot(p, dir);
                    float side = dot(p, sideDir);

                    float stretchX = mix(1.0, 1.35, speed);
                    float stretchY = mix(1.0, 0.88, speed);

                    vec2 stretched = vec2(along / stretchX, side / stretchY);

                    float angle = atan(stretched.y, stretched.x);
                    float dist = length(stretched);

                    float r = 0.30;
                    r += sin(angle * 3.0 + time * 1.8) * 0.01;
                    r += sin(angle * 5.0 - time * 1.3) * 0.006;
                    r += cos(angle * 7.0 + time * 1.6) * 0.004;
                    r += sin(angle * 2.0 + time * 2.2) * speed * 0.004;

                    return dist - r;
                }

                void main() {
                    vec2 uv = vUv;
                    vec2 mouse = uMouse;
                    vec2 velocity = uVelocity;

                    float d = blob(uv, mouse, uTime, velocity, uAspect);
                    float mask = 1.0 - smoothstep(0.0, 0.08, d);

                    vec2 diff = uv - mouse;
                    diff.x *= uAspect;

                    float dist = length(diff);
                    vec2 dir = normalize(diff + vec2(0.0001));

                    float speed = length(vec2(velocity.x * uAspect, velocity.y));

                    float globalWaveX = sin((uv.y * 18.0) + uTime * 1.8) * 0.006;
                    float globalWaveY = cos((uv.x * 16.0) - uTime * 1.5) * 0.006;

                    float ripple = sin(dist * 50.0 - uTime * 5.0) * (0.003 + speed * 0.01);
                    float waveX = sin((uv.y + uTime * 0.8) * 20.0) * speed * 0.006;
                    float waveY = cos((uv.x - uTime * 0.6) * 18.0) * speed * 0.006;

                    vec2 warpedUv = uv
                        + dir * ripple * mask
                        + vec2(waveX, waveY) * mask
                        + vec2(globalWaveX, globalWaveY) * 0.35;

                    float shimmer1 = sin((warpedUv.x + warpedUv.y) * 30.0 + uTime * 2.5);
                    float shimmer2 = cos(warpedUv.y * 42.0 - uTime * 2.0);
                    float shimmer3 = sin(warpedUv.x * 55.0 + warpedUv.y * 18.0 - uTime * 3.2);

                    float highlight = shimmer1 * 0.5 + shimmer2 * 0.3 + shimmer3 * 0.2;
                    highlight = highlight * 0.5 + 0.5;
                    highlight *= mask;

                    float softGlow = smoothstep(0.35, 0.0, d) * 0.18;
                    float edge = 1.0 - smoothstep(0.0, 0.02, abs(d));
                    float alpha = mask * 0.22 + softGlow + edge * 0.08;

                    vec3 base = vec3(1.0);
                    vec3 color = base * (0.75 + highlight * 0.45);

                    if (uDebug > 0.5) {
                        vec3 outlineColor = vec3(1.0, 0.2, 0.2);
                        color = mix(color, outlineColor, edge);
                        alpha = max(alpha, edge);
                    }

                    gl_FragColor = vec4(color, alpha);
                }
            `
        });

        const geometry = new THREE.PlaneGeometry(2, 2);
        const mesh = new THREE.Mesh(geometry, material);
        scene.add(mesh);

        let lastX = 0.75;
        let lastY = 0.5;
        let frame = 0;

        function updateMouse(e: PointerEvent) {
            const rect = container.getBoundingClientRect();
            const x = (e.clientX - rect.left) / rect.width;
            const y = 1 - (e.clientY - rect.top) / rect.height;

            const vx = x - lastX;
            const vy = y - lastY;

            uniforms.uTargetMouse.value.set(x, y);
            uniforms.uTargetVelocity.value.set(vx, vy);

            lastX = x;
            lastY = y;
        }

        function resize() {
            const width = container.clientWidth;
            const height = container.clientHeight;
            renderer.setSize(width, height);
            uniforms.uAspect.value = width / height;
        }

        window.addEventListener('pointermove', updateMouse, { passive: true });
        window.addEventListener('resize', resize, { passive: true });

        const clock = new THREE.Clock();

        function animate() {
            uniforms.uTime.value = clock.getElapsedTime();

            uniforms.uMouse.value.lerp(uniforms.uTargetMouse.value, 0.04);
            uniforms.uVelocity.value.lerp(uniforms.uTargetVelocity.value, 0.08);
            uniforms.uTargetVelocity.value.multiplyScalar(0.9);

            renderer.render(scene, camera);
            frame = requestAnimationFrame(animate);
        }

        animate();

        return () => {
            cancelAnimationFrame(frame);
            window.removeEventListener('pointermove', updateMouse);
            window.removeEventListener('resize', resize);
            geometry.dispose();
            material.dispose();
            renderer.dispose();
            container.removeChild(renderer.domElement);
        };
    });
</script>

<style>
    .wrap {
        position: absolute;
        inset: 0;
        z-index: 1;
        pointer-events: none;
        overflow: hidden;
    }

    .wrap :global(canvas) {
        display: block;
        width: 100%;
        height: 100%;
        pointer-events: none;
    }
</style>

<div bind:this={container} class="wrap"></div>