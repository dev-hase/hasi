<template>
    <figure class="placeholder">

        <cld-image
            :public-id="cldimage"
            crop="fill"
            gravity="auto:subject"
            fetchFormat="auto"
            loading="lazy"
            quality="auto"
            :alt="image"
            class="border-4 border-black cldimage"     
            width="1024"       
        >
            <cld-placeholder type="pixelate" />
        </cld-image>

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

};  
</script>

<style lang="stylus" scoped>

.placeholder
    background #000
    min-height 20rem


</style>