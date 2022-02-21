<template>
  <div>
    <div v-for="page in pages" :key="page.slug">
        <h1>{{page.title}}</h1>
        <nuxt-content :document="page" />
        <div>{{page.description}}</div>
    </div>
  </div>
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


