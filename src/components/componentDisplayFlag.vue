<template>
    <span>
        <img :src="showIcon(language)" :alt="language" class="icon-flag" @error="detectErrorFlag($event)">
    </span>
</template>
  
  
<script>

export default {
    name: 'componentDisplayFlag',
    props: {
        language: String,
    },
    methods: {
        showIcon(language) {
            language = this.convertLanguageCode(language);
            return `https://flagicons.lipis.dev/flags/1x1/${language}.svg`;
        },
        convertLanguageCode(language) {
            switch (language) {
                case 'ja': {
                    language = 'jp';
                    break;
                }
                case 'en': {
                    language = 'gb';
                    break;
                }
            }
            return language;
        },
        detectErrorFlag(event) {
            event.target.src = `https://flagicons.lipis.dev/flags/1x1/xx.svg`;
        },

    },
}
</script>
  
  
<style lang="scss" scoped>
.icon-flag {
    max-width: 12px;
}
</style>
  