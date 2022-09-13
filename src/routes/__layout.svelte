<script lang="ts">
    import "../app.css";
    import Header from "@lib/components/Header.svelte";
</script>

<Header />

<main class="background-image min-h-full">
    <slot />
</main>

<main class="background-image min-h-full">
    <slot />
</main>

<main class="background-image min-h-full">
    <slot />
</main>

<main class="background-image min-h-full">
    <slot />
</main>

<footer class="bg-astro-orange">
	<p class="flex justify-center">© Copyright 2022 ¤ Astrocrab AS ¤ All right reserved</p>
</footer>

<style>
    .background-image {
        background-image: url('/backgrounds/spacyspace.png');
        background-size: cover;
    }
</style>
