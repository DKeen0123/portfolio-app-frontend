<script>
  import { onMount } from "svelte";

  const getCryptos = async () => {
    const response = await fetch(
      "https://api.coingecko.com/api/v3/coins/markets?vs_currency=usd&order=market_cap_desc&per_page=100&page=1&sparkline=false"
    );
    const cryptos = await response.json();

    if (response.ok) {
      return cryptos;
    } else {
      throw new Error(cryptos);
    }
  };

  let top100Cryptos = getCryptos();
</script>

<svelte:head>
  <title>Fiscus</title>
</svelte:head>

<h1>Fiscus</h1>

<div class="coin-search">
  <h3>Select a coin:</h3>
  <select>
    {#await top100Cryptos}
      <option>...loading</option>
    {:then cryptos}
      {#each cryptos as { name }, i}
        <option>{name}</option>
      {/each}
    {:catch error}
      <p style="color: red">{error.message}</p>
    {/await}
  </select>
</div>

<style>
  .coin-search {
    text-align: center;
  }

  h1 {
    text-align: center;
    margin: 0 auto;
  }

  h1 {
    font-size: 2.8em;
    text-transform: uppercase;
    font-weight: 700;
    margin: 0 0 0.5em 0;
  }

  @media (min-width: 480px) {
    h1 {
      font-size: 4em;
    }
  }
</style>
