<template>
    <div>
        <p> TITOLO: {{ title }} </p>
        <p> TITOLO ORIGINALE: {{ originalTitle }} </p>
        <p>
            LINGUA ORIGINALE:
            <componentDisplayFlagVue :language="language" />
        </p>
        <p> VOTO: {{ vote }} </p>
        <componentImageVue :image="image" />
    </div>
</template>
  
  
<script>
import componentDisplayFlagVue from '@/components/componentDisplayFlag.vue';
import componentImageVue from '@/components/componentImage.vue';

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
}
</script>
  
  
<style lang="scss" scoped>

</style>
  