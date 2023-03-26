<template>
    <Page>
        <ActionBar>
            <Label text="Converter"/>
        </ActionBar>

        <GridLayout columns="*, *" rows="*, *, *">
            <Button @tap='goToMass' text="Масса" row="0" col="0"></Button>
            <Button text="Темпа" row="0" col="1"></Button>
            <Button text="Валюта" row="1" col="0"></Button>
            <Button text="Длинна" row="1" col="1"></Button>
            <Button text="Скорость" row="2" col="0"></Button>
            <Button text="Время" row="2" col="1"></Button>
        </GridLayout>
        
        
    </Page>
</template>

<script>
// import { GridLayout } from '@nativescript/core';
    import Mass from './Mass.vue'
    export default {
    data() {
        return {
            massPage: Mass
        };
    },
    methods: {
        
        goToMass(){
            this.$navigateTo(Mass)
        }

    },   
}

// const Mass = {
//         template: 
//             <template>
//                 <Page>
//                     <ActionBar>
//                         <Label text="По идее тут страница"/>
//                     </ActionBar>
//                 </Page>
//             </template>
        

//     };

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
