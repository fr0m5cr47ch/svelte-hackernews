<script>
  import Summary from "./Summary.svelte"
  import Spinner from "./Spinner.svelte"

  const PAGE_SIZE = 20

  export let page

  let items;
  let offset

  $: fetch(`https://node-hnapi.herokuapp.com/news?page=${page}`)
    .then(r => r.json())
    .then(data => {
      items = data;
      offset = PAGE_SIZE * (page - 1)
    })
</script>

<style>

    .paginator {
        padding: 2rem 0;
        text-align: center;
    }
    .paginator a {
        text-decoration: none;
        color: #666666;
        font-size: 1.5rem;
    }
    .paginator a[href] {
        color: #ffffff;
    }
    @keyframes fade-in {
        from { opacity: 0; }
        to { opacity: 1; }
    }
</style>

{#if items}
    {#each items as item, i}
        <Summary {item}/>
    {/each}
    <div class="paginator">
        <a href={page > 1 ? `#/top/${page - 1}` : null }>&lt;</a> |
        <a href={page < 10 ? `#/top/${page + 1}` : null }>&gt;</a>
    </div>
{:else}
    <Spinner/>
{/if}
