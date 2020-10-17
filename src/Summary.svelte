<script>
  export let item;

  $: url = item.type === "ask" ? `https://news.ycombinator.com/${item.url}` : item.url;
</script>

<style>
    article {
        position: relative;
    }

    h2 {
        font-size: 1em;
        margin: 0.5em 0;
    }

    span {
        position: absolute;
        left: 0;
    }

    a {
        color: #333;
    }
</style>

<article>
    <h2><a target="_blank" href={url}>{item.title}</a> | <a href="#/item/{item.id}">🗨 {item.comments_count}</a> | {item.user} {item.time_ago}</h2>
</article>
