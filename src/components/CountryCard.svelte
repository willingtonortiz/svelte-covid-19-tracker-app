<script lang="ts">
	interface Country {
		country?: string;
		cases?: number;
		deaths?: number;
		recovered?: number;
	}

	export let isDark: boolean = false;
	export let country: Country = {};
	let flagUrl: string = "";

	$: {
		fetchCountryFlagImageUrl(country.country).then((imageUrl: string) => {
			flagUrl = imageUrl;
		});
	}

	const fetchCountryFlagImageUrl = async (countryName: string) => {
		const url = `https://restcountries.eu/rest/v2/name/${countryName}`;
		const response = await fetch(url, { method: "GET" });
		const jsonResponse = await response.json();
		return jsonResponse[0].flag;
	};
</script>

<style>
	.container {
		padding: 48px 0;
		background-color: #eaeaea;

		display: flex;
		flex-flow: column nowrap;
		align-items: center;
	}

	.container.dark {
		background-color: #474747;
	}

	.container img {
		margin-bottom: 12px;
		width: 150px;
		height: 100px;
	}

	.container h1 {
		font-size: 28px;
	}
	.container.dark h1 {
		color: #eeeeee;
	}

	.container p {
		font-size: 20px;
	}
	.container.dark p {
		color: #eeeeee;
	}
</style>

<div class="container {isDark ? 'dark' : ''}">
	<img src={flagUrl} alt="country flag" />
	<h1>{country.country}</h1>
	<p>Total de casos: {country.cases}</p>
	<p>Total de muertes: {country.deaths}</p>
	<p>Total de recuperados: {country.recovered}</p>
</div>
