<template>
    <img :src="makeDisplayImage()" alt="image cover content">
</template>
  
  
<script>

export default {
    name: 'componentImage',
    props: {
        image: String,
        size: Number,
    },
    methods: {
        makeDisplayImage() {
            return 'https://image.tmdb.org/t/p/w' + this.size + this.image;
        }
    }
}
</script>
  
  
<style lang="scss" scoped>
img {
    width: 100px;
}
</style>