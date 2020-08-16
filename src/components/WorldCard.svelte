<script lang="ts">
	export let isDark: boolean = true;
	export let worldInfo: any = {
		cases: 0,
		deaths: 0,
		recovered: 0,
	};
</script>

<style>
	.container {
		padding: 24px 0;
		display: grid;
		grid-template-columns: repeat(3, 1fr);

		background-color: #34495e;
	}
	.container.dark {
		background-color: #302f2f;
	}

	.container .group {
		display: flex;
		flex-flow: column nowrap;
		align-items: center;
	}

	.container .group img {
		width: 70px;
		height: 70px;
	}

	.container .group p {
		color: #eeeeee;
		font-size: 22px;
	}

	@media only screen and (max-width: 600px) {
		.container {
			grid-template-columns: 1fr;
			grid-template-rows: repeat(3, 1fr);
		}
		.container .group {
			margin-bottom: 28px;
		}
	}
</style>

<div class="container {isDark ? 'dark' : ''}">
	<div class="group">
		<img src="/assets/totalcases.png" alt="Casos totales" />
		<p>Total de casos</p>
		<p>{worldInfo.cases}</p>
	</div>

	<div class="group">
		<img src="/assets/deaths.png" alt="Casos totales" />
		<p>Total de Muertes</p>
		<p>{worldInfo.deaths}</p>
	</div>

	<div class="group">
		<img src="/assets/recovered.png" alt="Casos totales" />
		<p>Total de Recuperados</p>
		<p>{worldInfo.recovered}</p>
	</div>
</div>
