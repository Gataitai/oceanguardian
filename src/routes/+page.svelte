<script lang="ts">
    import { onMount } from 'svelte'
    import { fly } from 'svelte/transition'
    import BannerWater from '../components/BannerWater.svelte'
    import Photos from '../components/Photos.svelte'
    import bannerUrl from '$lib/assets/banner.png'
//
    let comboElements: HTMLDivElement[] = []
    let visible = $state([false, false, false, false, false, false, false])

    onMount(() => {
        const observer = new IntersectionObserver(
            (entries) => {
                for (const entry of entries) {
                    if (entry.isIntersecting) {
                        const index = comboElements.findIndex((element) => element === entry.target)
                        if (index !== -1) {
                            visible[index] = true
                            observer.unobserve(entry.target)
                        }
                    }
                }
            },
            {
                threshold: 0.15
            }
        )

        for (const element of comboElements) {
            if (element) observer.observe(element)
        }

        return () => observer.disconnect()
    })
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
        padding: 7rem 10rem;
    }

    .section-inner {
        display: flex;
        justify-content: space-between;
        gap: 2rem;
    }

    .section-inner.with-photos {
        min-height: 100vh;
    }

    .left,
    .right {
        display: flex;
        flex-direction: column;
        flex: 1;
        width: 50%;
    }

    .combo + .combo {
        margin-top: 3.5rem;
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

    .left p + a,
    .right p + a {
        margin-top: 1.5rem;
    }

    .left a,
    .right a {
        align-self: flex-start;
    }

    .combo-placeholder {
        visibility: hidden;
    }

    .banner {
        min-height: 100vh;
        display: flex;
        align-items: center;
        padding: 10rem;
        position: relative;
        background: var(--orange);
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

    .photos-side {
        display: flex;
        align-items: center;
        min-height: 100vh;
    }

    .photos-side.left {
        justify-content: flex-start;
    }

    .photos-side.right {
        justify-content: flex-end;
    }

    .footer {
        background: var(--darkest);
        color: var(--white);
        display: flex;
        justify-content: space-between;
        align-items: center;
        padding: 2rem 10rem;
        gap: 2rem;
        flex-wrap: wrap;
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
        <div class="section-inner with-photos">
            <div class="left">
                <div class="combo" bind:this={comboElements[0]}>
                    {#if visible[0]}
                        <div transition:fly={{ y: 80, duration: 700 }}>
                            <h2>What is this experience</h2>
                            <p>Ocean Guardian offers a unique family experience, where travel, education, and conservation come together.</p>
                            <p>Join hands-on coral workshops, explore local Balinese life, snorkel in calm waters, and even plant coral with your family.</p>
                            <p>It is designed to be fun, meaningful, and unforgettable for both parents and children.</p>
                        </div>
                    {:else}
                        <div class="combo-placeholder">
                            <h2>What is this experience</h2>
                            <p>Ocean Guardian offers a unique family experience, where travel, education, and conservation come together.</p>
                            <p>Join hands-on coral workshops, explore local Balinese life, snorkel in calm waters, and even plant coral with your family.</p>
                            <p>It is designed to be fun, meaningful, and unforgettable for both parents and children.</p>
                        </div>
                    {/if}
                </div>

                <div class="combo" bind:this={comboElements[1]}>
                    {#if visible[1]}
                        <div transition:fly={{ y: 80, duration: 700 }}>
                            <h2>What makes this special</h2>
                            <p>Guided by a doctoral marine researcher, you will learn directly from experts working on real coral restoration.</p>
                            <p>Designed by parents, and supported by a personal development coach, this journey focuses on both environmental impact and family connection.</p>
                        </div>
                    {:else}
                        <div class="combo-placeholder">
                            <h2>What makes this special</h2>
                            <p>Guided by a doctoral marine researcher, you will learn directly from experts working on real coral restoration.</p>
                            <p>Designed by parents, and supported by a personal development coach, this journey focuses on both environmental impact and family connection.</p>
                        </div>
                    {/if}
                </div>
            </div>

            <div class="right photos-side right">
                <Photos align="right" />
            </div>
        </div>
    </section>

    <section class="section sea">
        <div class="section-inner with-photos">
            <div class="left photos-side left">
                <Photos align="left" />
            </div>

            <div class="right">
                <div class="combo" bind:this={comboElements[2]}>
                    {#if visible[2]}
                        <div transition:fly={{ y: 80, duration: 700 }}>
                            <h2>Where and when</h2>
                            <p>The program takes place from 7 to 10 June, in North Bali, around Lovina and Singaraja, aligned with Coral Triangle Day.</p>
                            <p>Enjoy sunrise dolphin watching, explore Bali’s former capital, and experience a quieter, more authentic side of the island.</p>
                        </div>
                    {:else}
                        <div class="combo-placeholder">
                            <h2>Where and when</h2>
                            <p>The program takes place from 7 to 10 June, in North Bali, around Lovina and Singaraja, aligned with Coral Triangle Day.</p>
                            <p>Enjoy sunrise dolphin watching, explore Bali’s former capital, and experience a quieter, more authentic side of the island.</p>
                        </div>
                    {/if}
                </div>

                <div class="combo" bind:this={comboElements[3]}>
                    {#if visible[3]}
                        <div transition:fly={{ y: 80, duration: 700 }}>
                            <h2>Who is it for</h2>
                            <p>Created for families who want more than a vacation, and are looking for a meaningful shared experience.</p>
                        </div>
                    {:else}
                        <div class="combo-placeholder">
                            <h2>Who is it for</h2>
                            <p>Created for families who want more than a vacation, and are looking for a meaningful shared experience.</p>
                        </div>
                    {/if}
                </div>

                <div class="combo" bind:this={comboElements[4]}>
                    {#if visible[4]}
                        <div transition:fly={{ y: 80, duration: 700 }}>
                            <h2>What you will do</h2>
                            <p>Learn coral restoration, connect with local communities, explore nature, and experience Bali through conservation and education.</p>
                        </div>
                    {:else}
                        <div class="combo-placeholder">
                            <h2>What you will do</h2>
                            <p>Learn coral restoration, connect with local communities, explore nature, and experience Bali through conservation and education.</p>
                        </div>
                    {/if}
                </div>
            </div>
        </div>
    </section>

    <section class="section dark">
        <div class="section-inner">
            <div class="left">
                <div class="combo" bind:this={comboElements[5]}>
                    {#if visible[5]}
                        <div transition:fly={{ y: 80, duration: 700 }}>
                            <h2>Why join</h2>
                            <p>This journey helps families reconnect with nature, while learning how to protect it in a practical way.</p>
                            <p>Instead of only visiting Bali, you actively contribute to preserving its marine life for future generations.</p>
                        </div>
                    {:else}
                        <div class="combo-placeholder">
                            <h2>Why join</h2>
                            <p>This journey helps families reconnect with nature, while learning how to protect it in a practical way.</p>
                            <p>Instead of only visiting Bali, you actively contribute to preserving its marine life for future generations.</p>
                        </div>
                    {/if}
                </div>
            </div>

            <div class="right">
                <div class="combo" bind:this={comboElements[6]}>
                    {#if visible[6]}
                        <div transition:fly={{ y: 80, duration: 700 }}>
                            <h2>How to join</h2>
                            <p>Fill in the form with your name, WhatsApp number, and email, or contact us directly.</p>
                            <a href="https://wa.me/6587511990" class="btn">Contact via WhatsApp</a>
                        </div>
                    {:else}
                        <div class="combo-placeholder">
                            <h2>How to join</h2>
                            <p>Fill in the form with your name, WhatsApp number, and email, or contact us directly.</p>
                            <a href="https://wa.me/6587511990" class="btn">Contact via WhatsApp</a>
                        </div>
                    {/if}
                </div>
            </div>
        </div>
    </section>

    <footer class="footer">
        <span>Cubulan© 2026. All rights reserved.</span>
        <span>Email: info@cubulan.com</span>
        <span>Phone: +65 8751 1990</span>
    </footer>
</div>