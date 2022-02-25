<template>
  <body class="bg-green-400">

    <div class="bg-green-600 text-center text-white text-7xl font-black p-6 ">Test Area</div>

    <div v-for="article in articles" :key="article.slug" class="bg-green-200 p-6 rounded-md mx-auto my-5 w-4/5 flex justify-center flex-col md:flex-row">
        <p class="font-black text-2xl py-2 md:pr-5">{{article.title}}</p>
 
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

        <div class="p-2 bg-black text-white font-medium md:w-1/4">{{article.description}}</div>

    </div>

    <button @click="$fetch" class="bg-green-600 text-white font-bold p-2 w-full">klick!</button>

  </body>
</template>

<script>

export default {

  data() {

    return {
      articles: [],
      pointer: 0
    }
  },

  // fetch()
  async fetch() {
    //const random = Math.floor(Math.random() * 7);
    //alert(random)

    this.newarticles = await this.$content("articles")
        .limit(3)
        .skip(this.pointer)
        .sortBy("slug", "desc")
        .fetch()
        .then((newarticles) => {
            this.articles.push(...newarticles);
            this.pointer += 3;
            //alert(this.pointer)

            //this.articles = newarticles.map((x) => x);
        })

  }


  
}

</script>