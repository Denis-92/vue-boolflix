<template>
    <div id="movies">
        <p> TITOLO: {{ content.title }} </p>
        <p> TITOLO ORIGINALE: {{ content.original_title }} </p>
        <p>
            LINGUA ORIGINALE:
            <componentDisplayFlagVue :language="content.original_language" />
        </p>
        <p> VOTO: {{ content.vote_average }} </p>
        <componentImageVue :image="content.poster_path" size="500" />
    </div>
</template>
  
  
<script>
import componentDisplayFlagVue from '@/components/componentDisplayFlag.vue';
import componentImageVue from '@/components/componentImage.vue';

export default {
    name: 'componentMovies',
    components: {
        componentDisplayFlagVue,
        componentImageVue,
    },
    props: {
        content: Object,
    },
}
</script>
  
  
<style lang="scss" scoped>

</style>
  