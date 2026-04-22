<script lang="ts">
    import logo from '$lib/assets/cubulan.png';

    let menuOpen = $state(false);

    function toggleMenu() {
        menuOpen = !menuOpen;
    }

    function closeMenu() {
        menuOpen = false;
    }
</script>

<style>
    :global(html) {
        scroll-behavior: smooth;
    }

    .navbar {
        position: absolute;
        top: 0;
        left: 0;
        width: 100%;
        box-sizing: border-box;
        padding: 2rem 10rem 0 10rem;
        display: flex;
        justify-content: space-between;
        align-items: center;
        font-family: 'Poppins', sans-serif;
        color: var(--white);
        z-index: 50;
    }

    .left {
        display: flex;
        align-items: center;
        gap: 2.5rem;
    }

    .right {
        display: flex;
        align-items: center;
        gap: 1.5rem;
    }

    a {
        color: var(--white);
        text-decoration: none;
        white-space: nowrap;
    }

    a:hover {
        color: var(--sand);
    }

    .logo {
        display: flex;
        align-items: center;
        height: 3rem;
    }

    .logo img {
        height: 100%;
        width: auto;
        object-fit: contain;
    }

    .cta {
        background: var(--orange);
        color: var(--dark);
        padding: 0.6rem 1.2rem;
        border-radius: 999px;
        font-weight: 600;
    }

    .cta:hover {
        background-color: var(--sea);
        color: var(--white);
    }

    .burger {
        display: none;
        background: transparent;
        border: none;
        cursor: pointer;
        width: 2.2rem;
        height: 2.2rem;
        flex-direction: column;
        gap: 0.35rem;
    }

    .burger span {
        display: block;
        width: 100%;
        height: 3px;
        background: var(--white);
    }

    .modal-backdrop {
        position: fixed;
        inset: 0;
        background: rgba(15, 23, 42, 0.96);
        z-index: 100;
        display: flex;
        justify-content: center;
        align-items: center;
    }

    .modal {
        display: flex;
        flex-direction: column;
        gap: 1rem;
        text-align: center;
    }

    .modal a {
        font-size: 1.5rem;
    }

    .close {
        position: absolute;
        top: 1.5rem;
        right: 1.5rem;
        background: transparent;
        border: none;
        color: var(--white);
        font-size: 2rem;
        cursor: pointer;
    }

    @media (max-width: 800px) {
        .left a:not(.logo),
        .right {
            display: none;
        }

        .burger {
            display: flex;
        }
    }
</style>

<nav class="navbar">
    <div class="left">
        <a class="logo" href="https://cubulan.com">
            <img src={logo} alt="logo" />
        </a>

        <a href="#experience" onclick={closeMenu}>Experience</a>
        <a href="#details" onclick={closeMenu}>Details</a>
        <a href="#why" onclick={closeMenu}>Why</a>
        <a href="#join" onclick={closeMenu}>Join</a>
    </div>

    <div class="right">
        <a href="https://wa.me/6587511990" onclick={closeMenu} class="cta">Contact now</a>
    </div>

    <button class="burger" onclick={toggleMenu}>
        <span></span>
        <span></span>
        <span></span>
    </button>
</nav>

{#if menuOpen}
    <div class="modal-backdrop">
        <button class="close" onclick={closeMenu}>×</button>

        <div class="modal">
            <a href="#experience" onclick={closeMenu}>Experience</a>
            <a href="#details" onclick={closeMenu}>Details</a>
            <a href="#why" onclick={closeMenu}>Why</a>
            <a href="#join" onclick={closeMenu}>Join</a>
            <a class="cta" href="#join" onclick={closeMenu}>Join Now</a>
        </div>
    </div>
{/if}