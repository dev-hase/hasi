<template>
  <body class="bg-pink-900">

    <div class="bg-pink-700 text-center text-white text-7xl font-black p-6">HASI</div>

    <div v-for="article in articles" :key="article.slug" class="p-6 mx-auto my-5 w-full md:w-4/5 flex justify-center flex-col md:flex-row">
        <p class="text-gray-200 font-black text-2xl py-2 md:pr-5">{{article.title}}</p>

        <nuxt-img 
          provider="cloudinary" 
          :src="'hasi/' + article.pic" 
          width="1200px"
          dpr="auto"
          crop="fill"
          fetchFormat="auto"
          quality="auto"
          loading="lazy"  
          class="border-2 border-black shadow-xl w-full md:w-3/4"
        />
              
        <nuxt-content :document="article" />

        <div class="p-2 bg-black text-gray-200 font-medium md:w-1/4">{{article.description}}</div>

    </div>

    <infinite-loading spinner="waveDots" @infinite="infiniteHandler">
      <div slot="no-more" class="text-pink-500 font-thinner text-sm">Ende!</div>
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

      }, 500);
    }

  }

  
}

</script>


