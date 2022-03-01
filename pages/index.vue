<template>
  <body class="bg-pink-900">

    <pageheader />

    <div v-for="article in articles" :key="article.slug" :class="'storie mx-auto w-full flex flex-autojustify-center flex-col ' + article.class">

        <div class="articleheader mx-5 mt-10 w-3/4 lg:w-3/5">

            <h1 class="pt-4 text-5xl md:text-7xl md:tracking-wider text-gray-200 font-black">{{article.title}}</h1>

            <div class="pt-4 pb-10 text-md md:text-xl text-gray-200 font-thinnest">{{article.description}}</div>

        </div>
 
        <nuxt-content :document="article" class="text-gray-300 italic text-right leading-relaxed md:leading-loose tracking-narrow text-2xl md:text-3xl" />


    </div>

    <infinite-loading spinner="waveDots" @infinite="infiniteHandler">
      <div slot="no-more">
        <pageheader />
      </div>
      <div slot="no-results">nix gefunden</div>
    </infinite-loading>

  </body>
</template>

<script>
import Pageheader from "../components/pageheader.vue";

export default {
    data() {
        return {
            articles: [],
            pointer: 0,
            numberofarticles: 1,
        };
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
                        return { pointer, articles };
                    }
                    else {
                        $state.complete();
                    }
                });
            }, 500);
        }
    },
    components: { Pageheader }
}

</script>

<style>

.stories-mystic {
    background: #831843;
}

.stories-fresh {
    background: #077a5d;
}

.stories-dark {
    background: #060219;
}

.storie {
    padding: 0 .25rem;
}

@media screen and (min-width: 640px) {

  .storie {
      padding: 0 7.5vw;
  }

}

@media screen and (min-width: 1200px) {

  .storie {
      padding: 0 27.5%;
  }

}

.articleheader {
    border-top: 3px solid #eee;
    height: 40vh;
}
.nuxt-content p {
    padding: 7.5rem 2rem 3.2rem 2rem;
    margin-left: 20vw;
}

@media screen and (min-width: 1200px) {
  .nuxt-content p {
      padding: 5rem 3rem 3.2rem 0rem;
  }
}

.nuxt-content em {
    font-weight: thin;
    color: #831843;
    background: #fff;
    padding: .1rem .5rem;
}

</style>