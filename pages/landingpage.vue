<template>
  <body class="bg-gray-900 py-5">
    <div v-for="article in articles" :key="article.slug">
        <p>{{article.title}}</p>
 
        <nuxt-img :src="'/img/' + article.pic" width="1024px" />
               
        <nuxt-content :document="page" />

        <div>{{article.description}}</div>

    </div>

    <button @click="$fetch()" class="bg-red-300 text-white font-bold p-2">klick!</button>

  </body>
</template>


<script>


export default {

  data: () => ({
    articles: []
  }),

  methods: {

    sayhi() {
      alert('say hi');
      //this.fetchData;

    },

    showarticles() {
      //alert('infinite');

      setTimeout(async () => {
        //page.value += 1;
        let list = await this.$content("articles")
          .skip(1)
          .sortBy("slug", "desc")
          .fetch()

        alert(list);
        return (articles)


      }, 500);
    }

  },


  async fetch () {
    this.articles = await $content('articles')
    .limit(1)
    .sortBy("slug", "desc")
    .fetch();

    return {
      articles
    }
  }
  
}
</script>