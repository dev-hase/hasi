<template>
  <body class="bg-green-400">

    <div class="bg-green-600 text-center text-white text-7xl font-black p-6 ">Test Area</div>

    <div v-for="article in articles" :key="article.slug" class="bg-green-200 p-6 rounded-md mx-auto my-5 w-4/5 flex justify-center flex-col md:flex-row">
        <p class="font-black text-2xl py-2 md:pr-5">{{article.title}}</p>
 
        <nuxt-img provider="cloudinary" :src="'hasi/' + article.pic" width="1024px" class="border-2 border-black shadow-xl w-full md:w-3/4" />
               
        <nuxt-content :document="article" />

        <div class="p-2 bg-black text-white font-medium md:w-1/4">{{article.description}}</div>

    </div>

    <infinite-loading @infinite="infiniteHandler"></infinite-loading>

  </body>
</template>

<script>

export default {

  data() {

    return {
      articles: [],
      pointer: 0,
    }
  },

  methods: {

    infiniteHandler($state) {
      //alert(this.pointer);

      setTimeout(async () => {
        this.newarticles = await this.$content("articles")
          .limit(2)
          .skip(this.pointer)
          .sortBy("slug", "desc")
          .fetch()        
          .then((newarticles) => {
              if (newarticles.length > 0) {
                this.articles.push(...newarticles);
                this.pointer += 2;
                $state.loaded();
                return { pointer, articles}
              } else {
                $state.complete();
              }

          })

      }, 630);
    }

  }

  
}

</script>

