<script>
  export let comment;
</script>

<style>
    article {
        margin: 1em 0 0 0;
        padding: 1em 0 0 0;
        font-size: 14px;
        color: #ffffff;
    }

    .meta {
        color: #999999;
    }

    .replies {
        padding: 0 0 0 1em;
        color: #fff;
    }
</style>

<article>
    <p class="meta">{comment.user} {comment.time_ago}</p>

    {@html comment.content}

    <div class="replies">
        {#each comment.comments as child}
            <svelte:self comment={child}/>
        {/each}
    </div>
</article>
