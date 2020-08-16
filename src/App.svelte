<script lang="ts">
  import CountryList from "./components/CountryList.svelte";
  import WorldCard from "./components/WorldCard.svelte";

  const ALL_COUNTRIES_URL =
    "https://coronavirus-19-api.herokuapp.com/countries";
  const WORLD_URL = "https://coronavirus-19-api.herokuapp.com/all";

  let isDark: boolean = false;
  let countryName: string = "";
  let countries: any[] = [];
  let worldInfo: any = {};

  const fetchAllCountries = async (url: string) => {
    const response = await fetch(url, {
      method: "GET",
    });

    const countries = await response.json();
    countries.shift();
    return countries;
  };

  const fetchOneCountryByName = async (url: string) => {
    const response = await fetch(url, {
      method: "GET",
    });

    return await response.json();
  };

  const fetchWorldInformation = async (url: string) => {
    const response = await fetch(url, {
      method: "GET",
    });

    return await response.json();
  };

  const fetchAndLoadOneCountryByName = async (countryName: string) => {
    const countryResult = await fetchOneCountryByName(
      `${ALL_COUNTRIES_URL}/${countryName}`
    );
    countries = [countryResult];
  };

  const fetchAndLoadAllCountries = async () => {
    const countriesResult = await fetchAllCountries(ALL_COUNTRIES_URL);
    countries = countriesResult;
  };

  const fetchAndLoadWorldInfo = async () => {
    const worldInfoResponse = await fetchWorldInformation(WORLD_URL);
    worldInfo = worldInfoResponse;
  };

  const loadData = async () => {
    fetchAndLoadAllCountries();
    fetchAndLoadWorldInfo();
  };

  const onKeyPressHandler = (event) => {
    const keyCode = event.keyCode;
    if (keyCode === 13) {
      fetchAndLoadOneCountryByName(countryName);
    }
  };

  const onKeyUpHandler = (event) => {
    if (countryName === "") {
      fetchAndLoadAllCountries();
    }
  };

  loadData();
  // countries = [{}];
</script>

<style>
  main {
    height: auto;
    padding: 0 22px;
    background-color: #ffffff;

    display: flex;
    flex-flow: column nowrap;
  }
  main.dark {
    background-color: #18191a;
  }

  .country-name {
    margin: 24px 0;
    padding: 8px 12px;
    border: none;
    border-bottom: 2px solid black;

    font-size: 22px;
    align-self: center;
  }
  .country-name:focus {
    outline: none;
  }
  main.dark .country-name {
    background-color: #747474;
    color: #eeeeee;
  }
  main.dark .country-name::placeholder {
    color: #eeeeee;
  }
</style>

<main class={isDark ? 'dark' : ''}>
  <input type="checkbox" bind:checked={isDark} />

  <WorldCard {worldInfo} {isDark} />

  <input
    class="country-name"
    type="text"
    bind:value={countryName}
    on:keypress={onKeyPressHandler}
    on:keyup={onKeyUpHandler}
    placeholder="Buscar por país..." />

  <CountryList {countries} {isDark} />
</main>
