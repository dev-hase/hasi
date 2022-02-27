<template>
    <div>

        <nuxt-img 
          provider="cloudinary" 
          :src="cldimage"
          preload
          sizes="sm:100vw md:100vw lg:100vw xxl:100vw"
          dpr="auto"
          crop="fill"
          fetchFormat="auto"
          quality="auto"
          class="border-4 border-black w-full"
          width="100%"
        />        

    </div>    
</template>

<script>  
export default {

    props: ["image"],

    data () {
    return {
        cldimage: 'hasi/' + this.image,
    }
    },

};  
</script>