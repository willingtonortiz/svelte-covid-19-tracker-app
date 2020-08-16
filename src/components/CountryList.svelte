<script lang="ts">
	import CountryCard from "./CountryCard.svelte";

	export let isDark: boolean = false;
	export let countries: any[] = [];
</script>

<style>
	.container {
		display: grid;
		gap: 20px;
		grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
	}
</style>

<main class="container">
	{#each countries as country (country.country)}
		<CountryCard {country} {isDark} />
	{/each}
</main>
