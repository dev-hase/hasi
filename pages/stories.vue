<template>
  <body class="bg-pink-900">

    <div class="bg-pink-700 text-center text-white text-7xl font-black p-6 tracking-widest">HASI</div>

    <div v-for="article in articles" :key="article.slug" class="p-6 mx-auto my-5 w-full lg:w-3/5 flex flex-autojustify-center flex-col">

        <div class="articleheader mt-10 w-3/4">

            <h1 class="pt-4 text-5xl md:text-7xl md:tracking-wider text-gray-200 font-black">{{article.title}}</h1>

            <div class="pt-4 pb-10 text-md md:text-xl text-gray-200 font-thinnest">{{article.description}}</div>

        </div>
 
        <nuxt-content :document="article" class="text-gray-300 italic tracking-narrow text-2xl md:text-3xl" />


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
        this.newarticles = await this.$content("stories")
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

<style>

.articleheader {
    border-top: 3px solid #eee;
    height: 40vh;
}
.nuxt-content p {
    padding: 7.5rem 0 3.2rem 0;
}
.nuxt-content em {
    font-weight: bold;
    color: #831843;
    background: #fff;
    padding: .1rem .5rem;
}
.nuxt-content img {
    border: 2px solid #661334;
}
</style>