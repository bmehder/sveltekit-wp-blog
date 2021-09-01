<script context="module">
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
</script>

<h1>{@html post[0].title.rendered}</h1>
<p>Published on: {post[0].date}</p>
<p>{@html post[0].content.rendered}</p>

<style>
  :global(img) {
    max-width: 400px;
    height: auto;
  }
</style>
