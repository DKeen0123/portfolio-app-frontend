<script context="module">
  export async function preload({ params, query }) {
    // the `slug` parameter is available because
    // this file is called [slug].svelte
    const res = await this.fetch(
      `https://api.coingecko.com/api/v3/coins/${params.slug}`
    );
    const data = await res.json();

    if (res.status === 200) {
      return { crypto: data };
    } else {
      this.error(res.status, data.message);
    }
  }
</script>

<script>
  import Expandable from "../../components/ui/expandable/index.svelte";
  import Ticker from "../../components/ui/ticker/index.svelte";
  export let crypto;
  console.log(crypto);
  const marketData = crypto.market_data;
  const priceChangePercentage = marketData.price_change_percentage_24h;
</script>

<svelte:head>
  <title>{crypto.name}</title>
</svelte:head>

<Ticker {crypto} />

<Expandable header="Description" innerText={crypto.description.en} />
