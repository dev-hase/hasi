<template>
    <div>

        <nuxt-img 
          provider="cloudinary" 
          :src="cldimage"
          preload
          sizes="sm:640px lg:1024px xxl:1600px"
          dpr="auto"
          crop="fill"
          fetchFormat="auto"
          quality="auto"
          class="border-4 border-black w-full"
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