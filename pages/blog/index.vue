<template>
  <section class="w-full md:w-2/3 flex flex-col items-center px-3">
    <ul v-for="article in articles" :key="article.title">
      <li>
        <NuxtLink :to="getUrl(article)">{{ article.title }}</NuxtLink>
      </li>
    </ul>
  </section>
</template>

<script>
export default {
    async asyncData({ $content, params }) {
      const articles = await $content("articles").fetch();
      console.log(articles)
      return {
        articles,
      };
    },
    methods: {
      getUrl(article) {
        return `/blog/${article.slug}`
      }

    }
}
</script>

<style>
.container {
  margin: 0 auto;
  min-height: 100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.subtitle {
  font-weight: 300;
  font-size: 42px;
  color: #526488;
  word-spacing: 5px;
  padding-bottom: 15px;
}

.links {
  padding-top: 15px;
}
</style>

