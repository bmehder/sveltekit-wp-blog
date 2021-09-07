<script context="module">
  export const load = async ({ page, fetch }) => {
    const pageNumber = page.query.get('page') || 1
    const url = `https://xycharts.com/wp-json/wp/v2/posts?page=${pageNumber}`

    const res = await fetch(url)
    const posts = await res.json()

    return {
      props: {
        posts,
        pageNumber,
      },
    }
  }
</script>

<script>
  export let posts
  export let pageNumber
</script>

{#if posts}
  <section>
    {#each posts as { title, date, excerpt, slug }}
      <div>
        <h2>{title.rendered}</h2>
        <p><small>{date}</small></p>
        <p>
          {#if !excerpt}
            No excerpt
          {/if}
          {@html excerpt.rendered}
        </p>
        <p><a sveltekit:prefetch href="/{slug}">Read More &raquo;</a></p>
      </div>
    {/each}
  </section>
  {#if pageNumber > 1}
    <a class="btn" href="/?page={+pageNumber - 1}">Previous Page</a>
  {/if}
  <a class="btn" href="/?page={+pageNumber + 1}">Next Page</a>
{/if}

<style>
  div {
    margin: 2rem 0;
    border-bottom: 1rem solid #eee;
  }
  .btn {
    padding: 1em 2em;
    background: dodgerblue;
    color: white;
  }
</style>
