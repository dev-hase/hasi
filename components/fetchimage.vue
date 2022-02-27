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

    computed: {
        src() {
        return this.$cloudinary.image.url(
            this.cldimage,
            {
            gravity: 'auto:subject',
            crop: 'fill',
            width: '2000',
            }
        )
        },

        src620() {
        return this.$cloudinary.image.url(
            this.cldimage,
            {
            gravity: 'auto:subject',
            crop: 'fill',
            width: '620',
            }
        )
        },

        src1270() {
        return this.$cloudinary.image.url(
            this.cldimage,
            {
            gravity: 'auto:subject',
            crop: 'fill',
            width: '1270',
            }
        )
        },

        src1690() {
        return this.$cloudinary.image.url(
            this.cldimage,
            {
            gravity: 'auto:subject',
            crop: 'fill',
            width: '1690',
            }
        )
        },
        
    }


};  
</script>