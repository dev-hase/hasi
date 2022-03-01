<template>
  <body class="bg-pink-900">

    <div class="bg-pink-700 text-center text-white text-7xl font-black p-6 tracking-widest">HASI</div>

    <div v-for="article in articles" :key="article.slug" class="p-6 mx-auto my-5 w-full md:w-4/5 flex flex-autojustify-center flex-col md:flex-row">
        <p class="text-gray-200 font-black text-md py-2 md:pr-5">{{article.title}}</p>

        <fetchimage folder="hasi/" :image="article.pic"></fetchimage>
              
        <nuxt-content :document="article" />

        <div class="p-4 bg-black text-xl text-gray-200 font-medium md:w-1/4 xl:w-1/5 flex-none">{{article.description}}</div>

    </div>

    <infinite-loading spinner="waveDots" @infinite="infiniteHandler">
      <div slot="no-more" class="text-pink-900 font-thinner text-sm w-full p-16 bg-pink-600">HASI2022</div>
      <div slot="no-results">nix gefunden</div>
    </infinite-loading>

  </body>
</template>

<script>

export default {

  data() {

    return {
      articles: [],
      pointer: 0,
      numberofarticles: 2,

    }
  },

  methods: {

    infiniteHandler($state) {
      //alert(this.pointer);

      setTimeout(async () => {
        this.newarticles = await this.$content("articles")
          .limit(this.numberofarticles)
          .skip(this.pointer)
          .sortBy("slug", "desc")
          .fetch()        
          .then((newarticles) => {
              if (newarticles.length > 0) {
                this.articles.push(...newarticles);
                this.pointer += this.numberofarticles;
                $state.loaded();
                return { pointer, articles}
              } else {
                $state.complete();
              }

          })

      }, 500);
    }

  }

  
}

</script>




