<template>
<div >
  <div v-for="post in posts" class="prose prose:sm" >
    <h2>
        <NuxtLink :to="slugify(post.slug)">{{ post.title }}</NuxtLink>
      </h2>
    <span>{{post.createdAt }}</span>
     <p>
       {{ post.snippet }}...
      </p>
  </div>
</div>


</template>

<script>
export default {
  async asyncData ({ $content }) {
    let posts = await $content('articles').sortBy('createdAt', 'desc').fetch()
    return { posts }
  },
  methods: {
    slugify(slug) {
      return `blog/${slug}`;
    }
  }
}
</script>

<style>
</style>
