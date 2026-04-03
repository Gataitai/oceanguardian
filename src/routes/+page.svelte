<script lang="ts">
import BannerWater from "../components/BannerWater.svelte";
</script>

<style>
    .page {
        width: 100%;
        font-family: 'Poppins', sans-serif;
    }

    .section {
        width: 100%;
        min-height: 100vh;
        position: relative;
    }

    .banner {
        display: flex;
        align-items: center;
        justify-content: flex-start;
        padding-left: 7rem;
        overflow: hidden;
    }

    .card {
        position: relative;
        z-index: 2;
        max-width: 50%;
        color: white;
        pointer-events: auto;
    }

    .card h1 {
        font-size: 3rem;
        font-weight: 700;
        line-height: 1.1;
        margin-bottom: 1rem;
    }

    .card p {
        font-size: 1.2rem;
        margin-bottom: 2rem;
    }

    .btn {
        background: var(--orange);
        color: var(--dark);
        padding: 0.8rem 1.6rem;
        border-radius: 999px;
        text-decoration: none;
        font-weight: 600;
        display: inline-block;
    }

    .orange {
        background-color: var(--orange);
        color: var(--dark);
    }

    .sea {
        background-color: var(--sea);
        color: var(--white);
    }

    .center {
        display: flex;
        justify-content: center;
        align-items: center;
    }
</style>

<div class="page">
    <section class="section banner">
        <BannerWater />

        <div class="card">
            <h1>
                A FAMILY ADVENTURE <br />
                IN BALI <br />
                THAT CREATES REAL IMPACT
            </h1>

            <p>
                Explore nature together and learn how to protect it through hands-on experiences like coral restoration and environmental activities.
            </p>

            <a href="/signup" class="btn">Start Your Journey</a>
        </div>
    </section>

    <section class="section orange center">
        next section
    </section>

    <section class="section sea center">
        next section
    </section>
</div>