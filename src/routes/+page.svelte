<script lang="ts">
    import BannerWater from '../components/BannerWater.svelte';
    import bannerUrl from '$lib/assets/banner.png';
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
        padding: 10rem;
    }

    .section-inner {
        display: flex;
        justify-content: space-between;
    }

    .left,
    .right {
        display: flex;
        flex-direction: column;
    }

    .left {
        flex: 1;
    }

    .right {
        flex: 1;
    }

    .left h2,
    .right h2 {
        margin-bottom: 1.5rem;
        margin-top: 0;
    }

    .left p + p,
    .right p + p {
        margin-top: 1rem;
    }

    .left p + h2,
    .right p + h2 {
        margin-top: 2rem;
    }

    .left p + a,
    .right p + a {
        margin-top: 1.5rem;
    }

    .left a,
    .right a {
        align-self: flex-start;
    }

    .banner {
        min-height: 100vh;
        display: flex;
        align-items: center;
        padding: 10rem;
        overflow: hidden;
        position: relative;
        background: var(--orange);
    }

    .banner-img {
        position: absolute;
        inset: 0;
        width: 100%;
        height: 100%;
        object-fit: cover;
        object-position: center top;
        z-index: 0;
        display: block;
    }

    .banner:hover {
        color: var(--sand);
    }

    .card {
        position: relative;
        z-index: 2;
        max-width: 50%;
        color: var(--white);
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
        line-height: 1.5;
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
        line-height: 1.1;
    }

    .section p {
        font-weight: 300;
        font-size: 24px;
        line-height: 1.5;
        margin: 0;
    }

    @media (max-width: 1200px) {
        .section,
        .banner {
            padding: 4rem;
        }

        .card {
            max-width: 65%;
        }

        .card h1,
        .section h2 {
            font-size: 40px;
        }

        .card p,
        .section p {
            font-size: 22px;
        }
    }

    @media (max-width: 900px) {
        .section-inner {
            flex-direction: column;
            gap: 2rem;
        }

        .banner {
            flex-direction: column;
            align-items: flex-start;
            justify-content: center;
            gap: 2rem;
            min-height: auto;
            padding-top: 6rem;
            padding-bottom: 3rem;
        }

        .card {
            max-width: 100%;
        }
    }

    @media (max-width: 700px) {
        .section,
        .banner {
            padding: 3rem;
        }

        .card h1,
        .section h2 {
            font-size: 32px;
        }

        .card p,
        .section p {
            font-size: 18px;
        }
    }

    @media (max-width: 500px) {
        .section,
        .banner {
            padding: 2rem;
        }

        .card h1,
        .section h2 {
            font-size: 26px;
        }

        .card p,
        .section p {
            font-size: 16px;
            margin-bottom: 1.5rem;
        }

        .btn {
            width: 100%;
            text-align: center;
        }
    }
</style>

<div class="page">
    <section class="banner">
        <BannerWater imageUrl={bannerUrl} />

        <div class="card">
            <h1>
                A FAMILY ADVENTURE <br />
                IN BALI <br />
                THAT CREATES REAL IMPACT
            </h1>

            <p>
                Discover Bali together as a family, while contributing to real ocean restoration.
                Learn, explore, and create meaningful memories that go beyond a typical holiday.
            </p>

            <a href="https://wa.me/6587511990" class="btn">Contact via WhatsApp</a>
        </div>
    </section>

    <section class="section orange">
        <div class="section-inner">
            <div class="left">
                <h2>What is this experience</h2>
                <p>
                    Ocean Guardian offers a unique family experience, where travel, education, and conservation come together.
                </p>
                <p>
                    Join hands-on coral workshops, explore local Balinese life, snorkel in calm waters, and even plant coral with your family.
                </p>
                <p>
                    It is designed to be fun, meaningful, and unforgettable for both parents and children.
                </p>

                <h2>What makes this special</h2>
                <p>
                    Guided by a doctoral marine researcher, you will learn directly from experts working on real coral restoration.
                </p>
                <p>
                    Designed by parents, and supported by a personal development coach, this journey focuses on both environmental impact and family connection.
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
                    The program takes place from 7 to 10 June, in North Bali, around Lovina and Singaraja, aligned with Coral Triangle Day.
                </p>
                <p>
                    Enjoy sunrise dolphin watching, explore Bali’s former capital, and experience a quieter, more authentic side of the island.
                </p>

                <h2>Who is it for</h2>
                <p>
                    Created for families who want more than a vacation, and are looking for a meaningful shared experience.
                </p>

                <h2>What you will do</h2>
                <p>
                    Learn coral restoration, connect with local communities, explore nature, and experience Bali through conservation and education.
                </p>
            </div>
        </div>
    </section>

    <section class="section dark">
        <div class="section-inner">
            <div class="left">
                <h2>Why join</h2>
                <p>
                    This journey helps families reconnect with nature, while learning how to protect it in a practical way.
                </p>
                <p>
                    Instead of only visiting Bali, you actively contribute to preserving its marine life for future generations.
                </p>
            </div>

            <div class="right">
                <h2>How to join</h2>
                <p>
                    Fill in the form with your name, WhatsApp number, and email, or contact us directly.
                </p>

                <a href="https://wa.me/6587511990" class="btn">Contact via WhatsApp</a>
            </div>
        </div>
    </section>
</div>