<script context="module">
  console.log('server')
  export const load = async ({ page, fetch }) => {
    const slug = page.params.slug
    const url = `https://xycharts.com/wp-json/wp/v2/posts?slug=${slug}`

    const res = await fetch(url)
    const post = await res.json()

    return {
      props: {
        post,
      },
    }
  }
</script>

<script>
  export let post

  const title = post[0].title.rendered
  const date = post[0].date
  const content = post[0].content.rendered

  console.log('client')
</script>

{#if post}
  <h1>{@html title}</h1>
  <p>Published on: {date}</p>
  <p>{@html content}</p>
{/if}
