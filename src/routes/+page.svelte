<script lang="ts">
    import BannerWater from '../components/BannerWater.svelte';
</script>

<style>
    .page {
        width: 100%;
        font-family: 'Poppins', sans-serif;
    }

    .section {
        width: 100%;
        padding: 6rem 7rem;
    }

    .banner {
        height: 100vh;
        display: flex;
        align-items: center;
        padding: 0 7rem;
        overflow: hidden;
    }

    .card {
        position: relative;
        z-index: 2;
        max-width: 50%;
        color: var(--white);
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
        max-width: 40rem;
    }

    .btn {
        background: var(--orange);
        color: var(--dark);
        padding: 0.8rem 1.6rem;
        border-radius: 999px;
        text-decoration: none;
        font-weight: 600;
    }

    .btn:hover {
        background: var(--sea);
        color: var(--white);
    }

    .orange {
        background: var(--orange);
        color: var(--dark);
    }

    .sea {
        background: var(--sea);
        color: var(--white);
    }

    .dark {
        background: var(--dark);
        color: var(--white);
    }

    .section h2 {
        font-size: 2.2rem;
        margin-bottom: 1.5rem;
    }

    .section p {
        max-width: 50rem;
        margin-bottom: 1rem;
        line-height: 1.6;
    }

    @media (max-width: 1000px) {
        .section,
        .banner,
        .card {
            max-width: 100%;
        }

        .card h1 {
            font-size: 2.2rem;
        }
    }
</style>

<div class="page">
    <section class="banner">
        <BannerWater />

        <div class="card">
            <h1>
                A FAMILY ADVENTURE <br />
                IN BALI <br />
                THAT CREATES REAL IMPACT
            </h1>

            <p>
                Explore nature together and learn how to protect it through hands-on experiences like coral restoration.
            </p>

            <a href="/signup" class="btn">Start Your Journey</a>
        </div>
    </section>

    <section class="section orange">
        <h2>What is this experience</h2>

        <p>
            Ocean Guardian presents a unique family ocean program where adventure meets purpose. This is not just a holiday it is a chance to explore Bali while making a real difference.
        </p>

        <p>
            You and your family will learn about coral reefs take part in conservation workshops and even plant your own coral in the ocean.
        </p>

        <p>
            Experience local Balinese life snorkel in shallow waters and create meaningful memories together.
        </p>
    </section>

    <section class="section sea">
        <h2>Where and when</h2>

        <p>
            7 to 10 June in North Bali Lovina and Singaraja during Coral Triangle Day.
        </p>

        <p>
            Enjoy calm beaches dolphin watching at sunrise and explore Singaraja the former capital of Bali.
        </p>

        <h2>Who is it for</h2>

        <p>
            Designed for families created by parents and guided by marine scientists no experience needed.
        </p>
    </section>

    <section class="section dark">
        <h2>Why join</h2>

        <p>
            Turn your holiday into something meaningful learn protect and experience the ocean together.
        </p>

        <p>
            Activities include coral planting workshops snorkeling and local experiences.
        </p>

        <h2>How to join</h2>

        <p>
            Fill in your name WhatsApp and email and we will contact you.
        </p>

        <a href="https://wa.me/6587511990" class="btn">Contact via WhatsApp</a>
    </section>
</div>