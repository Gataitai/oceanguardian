<script lang="ts">
    import logo from '$lib/assets/cubulan.png';
</script>

<style>
    .navbar {
        position: absolute;
        top: 0;
        left: 0;

        width: 100%;
        height: 7rem;
        box-sizing: border-box;
        padding: 0 7rem;

        display: flex;
        justify-content: space-between;
        align-items: center;

        font-family: 'Poppins', sans-serif;

        color: var(--white);
        z-index: 10;
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
        opacity: 0.8;
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
        display: block;
    }

    .cta {
        background: var(--orange);
        color: var(--dark);
        padding: 0.6rem 1.2rem;
        border-radius: 999px;
        font-weight: 600;
    }

    .cta:hover {
        opacity: 0.9;
    }
</style>

<nav class="navbar">
    <div class="left">
        <a class="logo" href="/">
            <img src={logo} alt="logo" />
        </a>

        <a href="/">Home</a>
        <a href="/about">About</a>
        <a href="/programme">Programme</a>
        <a href="/impact">Impact</a>
        <a href="/contact">Contact</a>
    </div>

    <div class="right">
        <a href="/login">Login</a>
        <a class="cta" href="/signup">Join Now</a>
    </div>
</nav>