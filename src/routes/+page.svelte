<script lang="ts">
    import BannerWater from '../components/BannerWater.svelte';
</script>

<style>
    .page {
        width: 100%;
        font-family: 'Poppins', sans-serif;
        position: relative;
        overflow: hidden;
    }

    .section {
        width: 100%;
        padding: 6rem 7rem;
        position: relative;
        overflow: hidden;
    }

    .section-inner {
        display: flex;
        justify-content: space-between;
        gap: 4rem;
    }

    .left {
        flex: 1;
    }

    .right {
        flex: 1;
    }

    .banner {
        height: 100vh;
        display: flex;
        align-items: center;
        padding: 0 7rem;
        overflow: hidden;
        position: relative;
    }

    .card {
        position: relative;
        z-index: 2;
        max-width: 50%;
        color: var(--white);
    }

    .content {
        position: relative;
        z-index: 2;
        max-width: 50rem;
    }

    .card h1 {
        font-size: 48px;
        font-weight: 700;
        line-height: 1.1;
        margin-bottom: 1rem;
    }

    .card p {
        font-size: 24px;
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
        font-size: 48px;
        font-weight: 700;
        margin-bottom: 1rem;
    }

    .section p {
        margin-bottom: 1rem;
        font-weight: 300;
        font-size: 24px;
    }

    @media (max-width: 1000px) {
        .section,
        .banner {
            padding: 4rem 2rem;
        }

        .card,
        .content {
            max-width: 100%;
        }

        .card h1 {
            font-size: 2.2rem;
        }

        .section-inner {
            flex-direction: column;
            gap: 2rem;
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
        <div class="section-inner">
            <div class="left">
                <h2>What is this experience</h2>
                <p>
                    Ocean Guardian presents a family ocean experience where adventure learning and conservation come together.
                </p>
                <p>
                    Join coral workshops discover Bali local life snorkel in shallow waters and help plant coral with your family.
                </p>
                <p>
                    It is fun meaningful and made to create memories that last.
                </p>
            </div>

            <div class="right"></div>
        </div>
    </section>

    <section class="section sea">
        <div class="section-inner">
            <div class="left"></div>

            <div class="right">
                <h2>Where and when</h2>
                <p>
                    The program takes place from 7 to 10 June in North Bali in Lovina and Singaraja around Coral Triangle Day.
                </p>
                <p>
                    Enjoy sunrise dolphin watching in Lovina and discover Singaraja the former capital of Bali.
                </p>

                <h2>Who is it for</h2>
                <p>
                    Designed for families curated by parents and guided by marine scientists.
                </p>
            </div>
        </div>
    </section>

    <section class="section dark">
        <div class="section-inner">
            <div class="left">
                <h2>Why join</h2>
                <p>
                    This journey helps families connect with the ocean in a fun meaningful and educational way.
                </p>
                <p>
                    Instead of only visiting Bali you become part of protecting it.
                </p>
            </div>

            <div class="right">
                <h2>How to join</h2>
                <p>
                    Fill in the form with your name WhatsApp number and email or reach out directly on WhatsApp.
                </p>

                <a href="https://wa.me/6587511990" class="btn">Contact via WhatsApp</a>
            </div>
        </div>
    </section>
</div>