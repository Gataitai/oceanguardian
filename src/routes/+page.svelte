<script lang="ts">
    import banner from '$lib/assets/banner.png';
</script>

<style>
    .page {
        width: 100vw;
    }

    .section {
        width: 100vw;
        height: 100vh;
        display: block;
    }

    .banner {
        background-size: cover;
        background-position: center;
        background-repeat: no-repeat;
    }

    .blue-dark {
        background-color: var(--blue-dark);
    }

    .green {
        background-color: var(--green);
    }
</style>

<div class="page">
    <section
            class="section banner"
            style:background-image={`url(${banner})`}
    ></section>

    <section class="section blue-dark">g</section>
    <section class="section green">g</section>
    <section class="section blue-dark">g</section>
</div>