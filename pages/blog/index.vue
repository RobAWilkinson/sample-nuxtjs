<template>
  <section class="w-full md:w-2/3 flex flex-col items-center px-3">
    <h1>Test</h1>
    Lorem ipsum dolor sit amet consectetur adipisicing elit. Laboriosam ab exercitationem corporis laborum quod dicta consectetur. Odit ipsa, deleniti voluptate hic quo nobis nemo accusamus cumque esse dicta dolore! Nisi.
  </section>
</template>

<script>
export default {
    async asyncData({ $content, params }) {
      const articles = await $content("articles").fetch();
      return {
        articles,
      };
    },
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

