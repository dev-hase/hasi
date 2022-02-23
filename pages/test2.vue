<template>
  <body class="bg-gray-900 py-5">
    <div v-for="article in articles" :key="article.slug">
        <p>{{article.title}}</p>
 
        <nuxt-img :src="'/img/' + article.pic" width="1024px" />
               
        <nuxt-content :document="article" />

        <div>{{article.description}}</div>

    </div>

    <button @click="$fetch" class="bg-red-300 text-white font-bold p-2">klick!</button>

  </body>
</template>

<script>

export default {

  data() {

    return {
      articles: []
    }
  },

  // fetch()
  async fetch() {
      const random = Math.floor(Math.random() * 7);

    this.articles = await this.$content("articles").limit(1).skip(random).fetch();
    //alert('hi')
  }


  
}

</script>