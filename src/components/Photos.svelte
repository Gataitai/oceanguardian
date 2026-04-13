<script lang="ts">
    import { fade } from 'svelte/transition'

    type Props = {
        images?: [string, string, string]
        align?: 'left' | 'right'
    }

    let {
        images = [
            'https://picsum.photos/1000/1200?1',
            'https://picsum.photos/1000/1200?2',
            'https://picsum.photos/1000/1200?3'
        ],
        align = 'left'
    }: Props = $props()

    let activeImage = $state<string | null>(null)

    function openImage(image: string) {
        activeImage = image
    }

    function closeImage() {
        activeImage = null
    }

    function stopWheel(e: WheelEvent) {
        if (activeImage) e.preventDefault()
    }

    function stopTouch(e: TouchEvent) {
        if (activeImage) e.preventDefault()
    }

    function stopKeys(e: KeyboardEvent) {
        if (!activeImage) return

        const blockedKeys = [
            'ArrowUp',
            'ArrowDown',
            'PageUp',
            'PageDown',
            'Home',
            'End',
            ' ',
            'Spacebar'
        ]

        if (blockedKeys.includes(e.key)) {
            e.preventDefault()
        }
    }

    $effect(() => {
        if (activeImage) {
            window.addEventListener('wheel', stopWheel, { passive: false })
            window.addEventListener('touchmove', stopTouch, { passive: false })
            window.addEventListener('keydown', stopKeys)
        }

        return () => {
            window.removeEventListener('wheel', stopWheel)
            window.removeEventListener('touchmove', stopTouch)
            window.removeEventListener('keydown', stopKeys)
        }
    })
</script>

<div class="photos {align}">
    {#if align === 'left'}
        <div class="col single-col">
            <img src={images[0]} class="photo single" onclick={() => openImage(images[0])} alt="photo 1" />
        </div>

        <div class="col double-col">
            <img src={images[1]} class="photo top" onclick={() => openImage(images[1])} alt="photo 2" />
            <img src={images[2]} class="photo bottom" onclick={() => openImage(images[2])} alt="photo 3" />
        </div>
    {:else}
        <div class="col double-col">
            <img src={images[0]} class="photo top" onclick={() => openImage(images[0])} alt="photo 1" />
            <img src={images[1]} class="photo bottom" onclick={() => openImage(images[1])} alt="photo 2" />
        </div>

        <div class="col single-col">
            <img src={images[2]} class="photo single" onclick={() => openImage(images[2])} alt="photo 3" />
        </div>
    {/if}
</div>

{#if activeImage}
    <div class="backdrop" onclick={closeImage} in:fade={{ duration: 200 }} out:fade={{ duration: 200 }}>
        <img
                src={activeImage}
                class="preview"
                alt="opened photo"
                in:fade={{ duration: 250 }}
                out:fade={{ duration: 150 }}
        />
    </div>
{/if}

<style>
    .photos {
        display: flex;
        align-items: center;
        width: 100%;
        height: 100%;
        gap: 1rem;
    }

    .photos.left {
        justify-content: flex-start;
    }

    .photos.right {
        justify-content: flex-end;
    }

    .col {
        display: flex;
        flex-direction: column;
    }

    .double-col {
        gap: 3rem;
    }

    .single-col {
        justify-content: center;
        height: 100%;
    }

    .photos.left .single-col {
        margin-right: 2rem;
    }

    .photos.right .double-col {
        margin-right: 2rem;
    }

    .photo {
        width: 12em;
        height: 22rem;
        object-fit: cover;
        border-radius: 1.25rem;
        box-shadow: 0 1rem 2rem rgba(0, 0, 0, 0.2);
        cursor: pointer;
        transition: transform 0.25s ease;
        display: block;
    }

    .top {
        transform: rotate(-6deg);
    }

    .bottom {
        transform: rotate(5deg);
    }

    .single {
        transform: rotate(-4deg);
    }

    .top:hover {
        transform: rotate(-5deg) scale(1.08);
    }

    .bottom:hover {
        transform: rotate(4deg) scale(1.08);
    }

    .single:hover {
        transform: rotate(-5deg) scale(1.08);
    }

    .backdrop {
        position: fixed;
        inset: 0;
        background: rgba(0, 0, 0, 0.9);
        display: flex;
        align-items: center;
        justify-content: center;
        z-index: 9999;
        cursor: pointer;
    }

    .preview {
        max-width: 80vw;
        max-height: 80vh;
        object-fit: contain;
        border-radius: 1rem;
        pointer-events: none;
        display: block;
    }
</style>