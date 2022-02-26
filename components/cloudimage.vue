<template>
    <figure>

        <img :src="src" alt="" class="border-4 border-black w-full md:w-3/4" />

    </figure>    
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
            width: '1200',
            }
        )
        }
    }


};  
</script>