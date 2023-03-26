<template>
    <Page>
        <ActionBar>
            <Label text="Converter"/>
        </ActionBar>

        <Label text="Конвертер массы"></Label>
        
        
    </Page>
</template>

<script>
// import { GridLayout } from '@nativescript/core';

  
    export default {
    data() {
        return {};
    },
    methods: {
        
    },
}

</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';

    // Custom styles
    .fas {
        @include colorize($color: accent);
    }

    .info {
        font-size: 20;
        horizontal-align: center;
        vertical-align: center;
    }
</style>
