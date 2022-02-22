<template>
  <body class="bg-gray-900 py-5">
    <div v-for="page in pages" :key="page.slug" class="container mx-auto md:p-36">
        <p class="pb-4 text-yellow-300 bg-gray-900 text-4xl text-center font-black">{{page.title}}</p>
 
        <nuxt-img :src="'/landingpage/' + page.pic" width="1024px" />
               
        <nuxt-content :document="page" />

        <div class="w-2/3 mx-auto bg-gray-300 text-gray-900 p-2 m-4 shadow-xl rounded-md font-bold italic">{{page.description}}</div>

    </div>
  </body>
</template>

<script>
export default {
  name: 'IndexPage',

  async asyncData ({ $content }) {
    const pages = await $content('landing-page')
    .sortBy("slug", "desc")
    .fetch()

    return {
      pages
    }
  }
}
</script>

