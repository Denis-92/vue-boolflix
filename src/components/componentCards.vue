<template>
    <div class="relative">
        <componentImageVue :image="image" />
        <div class="description">
            <p> Titolo: {{ title }} </p>
            <p> Titolo originale: {{ originalTitle }} </p>
            <span>
                <componentDisplayFlagVue :language="language" />
            </span>
            <span> Voto: {{ displayRating() }} </span>
        </div>
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
.relative {
    position: relative
}

.description {
    opacity: 0;
    position: absolute;
    top: 0;
    left: 0;
    height: 100%;
    width: 100%;
    padding: 2rem 1rem;

    &:hover {
        background-color: black;
        color: white;
        opacity: 1;
    }
}
</style>
  