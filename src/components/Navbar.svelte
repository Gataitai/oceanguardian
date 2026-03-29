<script lang="ts">
    import logo from '$lib/assets/logo.png';
</script>

<style>
    .navbar {

        font-size: 20px;
        position: absolute;
        top: 0;
        left: 0;

        width: 100vw;
        height: 7rem;

        padding: 0 10rem 0 10rem;

        display: flex;
        flex-direction: row;
        justify-content: space-around;
        align-items: center;

        font-family: 'Poppins', sans-serif;
        gap: 5rem;
        z-index: 10;
    }

    a {
        color: inherit;
        text-decoration: none;
    }

    a:hover {
        text-decoration: underline;
    }

    .logo {
        height: 100%;
        display: flex;
        align-items: center;
    }

    .logo img {
        height: 7rem;
        width: auto;
        display: block;
    }
</style>

<nav class="navbar">
    <a class="logo" href="/">
        <img src={logo} alt="Cubulan logo" />
    </a>

    <a href="/">Home</a>
    <a href="/about">About</a>
    <a href="/programme">Programme</a>
    <a href="/signup">Signup</a>
    <a href="/contact">Contact</a>
</nav>