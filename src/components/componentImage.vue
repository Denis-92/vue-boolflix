<template>
    <img :src="makeDisplayImage()" alt="image cover content" @error="missingImage($event)">
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
        },
        missingImage(event) {
            event.target.src = 'https://image.shutterstock.com/image-vector/missing-picture-page-website-design-260nw-1552421075.jpg';
        },
    }
}
</script>
  
  
<style lang="scss" scoped>
img {
    width: 100px;
}
</style>