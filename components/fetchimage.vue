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
          class="w-full"
          width="1024px"
        />      

    </div>    
</template>

<script>  
export default {

    props: ["folder", "image"],

    data () {
    return {
        cldimage: this.folder + this.image,
    }
    },

};  
</script>