<template>
  <body class="bg-gray-100 py-5">
    <h1 class="bg-white font-black text-7xl p-5">Testarea</h1>
    <div v-for="article in articles" :key="article.slug" class="container mx-auto md:p-36">
        <p class="pb-4 text-yellow-300 bg-gray-900 text-4xl text-center font-black">{{article.title}}</p>
 
        <nuxt-img :src="'/img/' + article.pic" width="1024px" />
               
        <nuxt-content :document="article" />

        <div class="w-2/3 mx-auto bg-gray-300 text-gray-900 p-2 m-4 shadow-xl rounded-md font-bold italic">{{article.description}}</div>

    </div>

    <infinite-loading @infinite="infiniteHandler">
    </infinite-loading>

  </body>
</template>

<script>
export default {

  setup() {
    function fetchData() {
      return $content("articles")
        .limit(3)
        .sortBy("slug", "desc")
        .fetch();
    }
  },

  async asyncData ({ $content }) {
    const articles = await $content('articles')
    .sortBy("slug", "desc")
    .fetch()

    return {
      articles
    }
  }
}
</script>

