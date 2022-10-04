<template>
    <div id="seriesTV">
        <p> TITOLO: {{ content.name }} </p>
        <p> TITOLO ORIGINALE: {{ content.original_name }} </p>
        <p>
            LINGUA ORIGINALE:
            <componentDisplayFlagVue :language="content.original_language" />
        </p>
        <p> VOTO: {{ content.vote_average }} </p>
    </div>
</template>
  
  
<script>
import componentDisplayFlagVue from '@/components/componentDisplayFlag.vue';

export default {

    name: 'componentseriesTv',
    components: {
        componentDisplayFlagVue,
    },
    props: {
        content: Object,
    },
}
</script>
  
  
<style lang="scss" scoped>

</style>
  