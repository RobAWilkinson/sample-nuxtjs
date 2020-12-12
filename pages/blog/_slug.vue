<template>
		<div class="w-full px-4 md:px-6 text-xl text-gray-800 leading-normal" style="font-family:Georgia,serif;">

<article>
	<div class="font-sans">
		<p class="text-base md:text-sm text-green-500 font-bold">&lt; <a href="#" class="text-base md:text-sm text-green-500 font-bold no-underline hover:underline">BACK TO BLOG</a></p>
				<h1 class="font-bold font-sans break-normal text-gray-900 pt-6 pb-2 text-3xl md:text-4xl">{{ article.title }}</h1>
				<p class="text-sm md:text-base font-normal text-gray-600">Published {{ prettyDate(article.createdAt)}}</p>
	</div>
	<div class="prose">
          <nuxt-content :document="article" />

	</div>
</article>
		<div class="flex flex-row justify-between font-sans">
			<div class="text-left" v-if="prev">
				<span class="text-xs md:text-sm font-normal text-gray-600">&lt; Previous Post</span><br>
				<p><NuxtLink :to="prev.slug" class="break-normal text-base md:text-sm text-green-500 font-bold no-underline hover:underline">{{ prev.title }}</NuxtLink></p>
			</div>
			<div v-if="!prev"></div>

			<div class="text-right" v-if="next">
				<span class="text-xs md:text-sm font-normal text-gray-600">Next Post &gt;</span><br>
				<p><NuxtLink :to="next.slug" class="break-normal text-base md:text-sm text-green-500 font-bold no-underline hover:underline">{{ next.title }}</NuxtLink></p>
			</div>
		</div>
</div>
</template>

<script>
import moment from "moment"
export default {
  async asyncData({ $content, params }) {
	const [prev, next] = await $content('articles')
      .only(['title', 'slug'])
      .sortBy('createdAt', 'asc')
      .surround(params.slug)
      .fetch();
	const article = await $content("articles", params.slug).fetch();
    return {
	  article,
	  prev,
	  next
	};

  },
methods: {
    slugify(slug) {
      return `blog/${slug}`;
	},
	prettyDate(date) {
		return moment(date).format("MMMM DD, YYYY")
	}
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
.nuxt-content ul {
  @apply list-disc list-inside;
}
</style>