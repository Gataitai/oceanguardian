<script lang="ts">
    import { onMount } from 'svelte';
    import * as THREE from 'three';
    import bannerUrl from '$lib/assets/banner.png';

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
        container.appendChild(renderer.domElement);

        const loader = new THREE.TextureLoader();
        const texture = loader.load(bannerUrl);
        texture.minFilter = THREE.LinearFilter;
        texture.magFilter = THREE.LinearFilter;

        const uniforms = {
            uTexture: { value: texture },
            uMouse: { value: new THREE.Vector2(0.5, 0.5) },
            uTargetMouse: { value: new THREE.Vector2(0.5, 0.5) },
            uVelocity: { value: new THREE.Vector2(0.0, 0.0) },
            uTargetVelocity: { value: new THREE.Vector2(0.0, 0.0) },
            uTime: { value: 0 },
            uDebug: { value: DEBUG ? 1.0 : 0.0 }
        };

        const material = new THREE.ShaderMaterial({
            uniforms,
            vertexShader: `
				varying vec2 vUv;

				void main() {
					vUv = uv;
					gl_Position = vec4(position.xy, 0.0, 1.0);
				}
			`,
            fragmentShader: `
				uniform sampler2D uTexture;
				uniform vec2 uMouse;
				uniform vec2 uVelocity;
				uniform float uTime;
				uniform float uDebug;

				varying vec2 vUv;

				vec4 blurStrong(sampler2D tex, vec2 uv) {
					float o1 = 0.004;
					float o2 = 0.008;
					float o3 = 0.012;

					vec4 color = vec4(0.0);

					color += texture2D(tex, uv + vec2(-o3, -o3));
					color += texture2D(tex, uv + vec2( o3, -o3));
					color += texture2D(tex, uv + vec2(-o3,  o3));
					color += texture2D(tex, uv + vec2( o3,  o3));

					color += texture2D(tex, uv + vec2(-o2, 0.0));
					color += texture2D(tex, uv + vec2( o2, 0.0));
					color += texture2D(tex, uv + vec2(0.0, -o2));
					color += texture2D(tex, uv + vec2(0.0,  o2));

					color += texture2D(tex, uv + vec2(-o1, -o1));
					color += texture2D(tex, uv + vec2( o1, -o1));
					color += texture2D(tex, uv + vec2(-o1,  o1));
					color += texture2D(tex, uv + vec2( o1,  o1));

					color += texture2D(tex, uv);

					return color / 13.0;
				}

				float blob(vec2 uv, vec2 center, float time, vec2 velocity) {
					vec2 p = uv - center;

					float angle = atan(p.y, p.x);
					float dist = length(p);

					float r = 0.24;
					r += sin(angle * 3.0 + time * 1.8) * 0.01;
					r += sin(angle * 5.0 - time * 1.3) * 0.006;
					r += cos(angle * 7.0 + time * 1.6) * 0.004;

					return dist - r;
				}

				void main() {
					vec2 uv = vUv;
					vec2 mouse = uMouse;
					vec2 velocity = uVelocity;

					float d = blob(uv, mouse, uTime, velocity);
					float mask = 1.0 - smoothstep(0.0, 0.08, d);

					vec2 diff = uv - mouse;
					float dist = length(diff);
					vec2 dir = normalize(diff + vec2(0.0001));

					float speed = length(velocity);

					// global water distortion for blurred area
					float globalWaveX = sin((uv.y * 18.0) + uTime * 1.8) * 0.006;
					float globalWaveY = cos((uv.x * 16.0) - uTime * 1.5) * 0.006;

					// local stronger distortion near blob
					float ripple = sin(dist * 50.0 - uTime * 5.0) * (0.003 + speed * 0.01);
					float waveX = sin((uv.y + uTime * 0.8) * 20.0) * speed * 0.006;
					float waveY = cos((uv.x - uTime * 0.6) * 18.0) * speed * 0.006;

					vec2 blurredUv = uv + vec2(globalWaveX, globalWaveY);
					vec2 sharpUv = uv + dir * ripple * mask + vec2(waveX, waveY) * mask + vec2(globalWaveX, globalWaveY) * 0.35;

					vec4 sharp = texture2D(uTexture, sharpUv);
					vec4 blurred = blurStrong(uTexture, blurredUv);

					vec4 color = mix(blurred, sharp, mask);

					if (uDebug > 0.5) {
						float outline = 1.0 - smoothstep(0.0, 0.01, abs(d));
						vec3 outlineColor = vec3(1.0, 0.2, 0.2);
						color.rgb = mix(color.rgb, outlineColor, outline);
					}

					gl_FragColor = color;
				}
			`
        });

        const geometry = new THREE.PlaneGeometry(2, 2);
        const mesh = new THREE.Mesh(geometry, material);
        scene.add(mesh);

        let lastX = 0.5;
        let lastY = 0.5;

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
            renderer.setSize(container.clientWidth, container.clientHeight);
        }

        window.addEventListener('pointermove', updateMouse, { passive: true });
        window.addEventListener('resize', resize, { passive: true });

        const clock = new THREE.Clock();
        let frame = 0;

        function animate() {
            uniforms.uTime.value = clock.getElapsedTime();

            uniforms.uMouse.value.lerp(uniforms.uTargetMouse.value, 0.04);
            uniforms.uVelocity.value.lerp(uniforms.uTargetVelocity.value, 0.08);
            uniforms.uTargetVelocity.value.multiplyScalar(0.92);

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
            texture.dispose();
            renderer.dispose();
            container.removeChild(renderer.domElement);
        };
    });
</script>

<style>
    .wrap {
        position: absolute;
        inset: 0;
        z-index: 0;
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