<script context="module">
  export const load = async ({ fetch }) => {
    const url = 'https://xycharts.com/wp-json/wp/v2/posts'

    const res = await fetch(url)
    const posts = await res.json()

    return {
      props: {
        posts,
      },
    }
  }
</script>

<script>
  export let posts
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
{/if}

<style>
  div {
    margin: 2rem 0;
    border-bottom: 1rem solid #eee;
  }
</style>
