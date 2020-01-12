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
  export let crypto;
  console.log(crypto);
</script>

<svelte:head>
  <title>{crypto.name}</title>
</svelte:head>

<h1>{crypto.name}</h1>

<Expandable header="Description" innerText={crypto.description.en} />
