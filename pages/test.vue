<template>
  <body>
    <h1 class="bg-red-500 text-white font-black text-7xl p-5">Testarea</h1>
    <div v-for="article in articles" :key="article.slug" class="container mx-auto md:p-36">
        <p class="pb-4 text-yellow-300 bg-gray-900 text-4xl text-center font-black">{{article.title}}</p>
 
        <nuxt-img :src="'/img/' + article.pic" width="1024px" />
               
        <nuxt-content :document="article" />

        <div class="w-2/3 mx-auto bg-gray-300 text-gray-900 p-2 m-4 shadow-xl rounded-md font-bold italic">{{article.description}}</div>

    </div>

    <button @click="sayhi()" class="bg-red-300 text-white font-bold p-2">klick!</button>

    <infinite-loading @infinite="infiniteHandler"></infinite-loading>

  </body>
</template>

<script>


export default {

 
  methods: {
    sayhi() {
      alert('say hi');
      //this.fetchData;

    },

    infiniteHandler($state) {
      //alert('infinite');

      setTimeout(async () => {
        //page.value += 1;
        let additionalItems = await this.$content("articles")
          .limit(3)
          .skip(3)
          .sortBy("slug", "desc")
          .fetch();

        alert(additionalItems);

        if (additionalItems.length > 0) {
          this.articles.value.push(...additionalItems);
          return{ articles };

          $state.loaded();
        } else {
          $state.complete();
        }
      }, 500);
    }


  },

  async asyncData ({ $content }) {
    const articles = await $content('articles')
    .limit(2)
    .sortBy("slug", "desc")
    .fetch()

    return {
      articles
    }
  }
}
</script>

<style lang="stylus" scoped>

body 
  background #eee
  padding 2vw

</style>
