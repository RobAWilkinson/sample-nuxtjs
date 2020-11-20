<template>
  <section class="w-full md:w-2/3 flex flex-col items-center px-3">
    <article class="flex flex-col shadow my-4">
      <div v-if="article.image">
        <a href="#" class="hover:opacity-75">
          <img
            src="https://source.unsplash.com/collection/1346951/1000x500?sig=1"
          />
        </a>
      </div>
      <div class="bg-white flex flex-col justify-start p-6">
        <a href="#" class="text-3xl font-bold hover:text-gray-700 pb-4">{{
          article.title
        }}</a>
        <p href="#" class="text-sm pb-8">
          By
          <a href="#" class="font-semibold hover:text-gray-800">{{
            article.author
          }}</a
          >, Published on {{ article.createdAt }}
        </p>

        <nuxt-content :document="article" />
      </div>
    </article>
  </section>
</template>

<script>
export default {
  async asyncData({ $content, params }) {
    const article = await $content("articles", params.slug).fetch();
    console.log(article);
    return {
      article,
    };
  },
  layout: "blog",
};
</script>

<style>
.nuxt-content h1 {
  @apply text-2xl font-bold pb-3;
}
.nuxt-content p {
  @apply pb-3;
}
</style>