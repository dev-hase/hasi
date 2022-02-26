<template>
    <div>


        <picture>
            <img
            sizes="(max-width: 1690px) 100vw, 1690px"
            :srcset="src620 + ' 620w, ' + src1270 + ' 1270w,' + src1690 + ' 1690w'"
            :src="src"
            :alt="image" />
        </picture>


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