<template>
    <div>
        <p> TITOLO: {{ title }} </p>
        <p> TITOLO ORIGINALE: {{ originalTitle }} </p>
        <p>
            LINGUA ORIGINALE:
            <componentDisplayFlagVue :language="language" />
        </p>
        <p> VOTO: {{ displayRating() }} </p>
        <componentImageVue :image="image" />
    </div>
</template>
  
  
<script>
import componentDisplayFlagVue from '@/components/componentDisplayFlag.vue';
import componentImageVue from '@/components/componentImage.vue';

const CONVERT_OUT_OF_5 = 2;

export default {
    name: 'componentCards',
    components: {
        componentDisplayFlagVue,
        componentImageVue,
    },
    props: {
        title: String,
        originalTitle: String,
        language: String,
        vote: Number,
        image: String,
    },
    methods: {
        displayRating() {
            return Math.ceil(this.vote / CONVERT_OUT_OF_5);
        }
    },
}
</script>
  
  
<style lang="scss" scoped>

</style>
  