<template>
    <Page>
        <ActionBar>
            <Label text="Converter"/>
        </ActionBar>
        <GridLayout class="back_buttons" columns="*, *" rows="*, *, *">   
            <button class="button-home" row="0" col="0" @tap="goToMass" text="Масса" backgroundImage="~/assets/mass.png" />
            <button class="button-home" row="0" col="1" @tap="goToTemp" text="Температура" backgroundImage="~/assets/temp.png" />
            <button class="button-home" row="1" col="0" @tap="goToSpeed" text="Скорость" backgroundImage="~/assets/speed.png" />
            <button class="button-home" row="1" col="1" @tap="goToTime" text="Время" backgroundImage="~/assets/time.png" />
            <button class="button-home" row="2" col="0" @tap="goToCurr" text="Валюта" backgroundImage="~/assets/curr.png" />
            <button class="button-home" row="2" col="1" @tap="goToLong" text="Длинна" backgroundImage="~/assets/long.png" />
        </GridLayout>
        
        
    </Page>
</template>

<script>


import Mass from './Mass.vue'
import Temp from './Temp.vue'
import Speed from './Speed.vue'
import Time from './Time.vue'
import Currency from './Currency.vue'
import Long from './Long.vue'
    export default {
    data() {
        return {};
    },
    methods: {
        goToMass() {
            this.$navigateTo(Mass);
        },

        goToTemp() {
            this.$navigateTo(Temp);
        },

        goToSpeed() {
            this.$navigateTo(Speed);
        },

        goToTime() {
            this.$navigateTo(Time);
        },

        goToCurr() {
            this.$navigateTo(Currency);
        },

        goToLong() {
            this.$navigateTo(Long);
        },
       
    },
   
}

</script>

<style scoped lang="scss">
    @import '@nativescript/theme/scss/variables/blue';

    // Custom styles
    .fas {
        @include colorize($color: accent);;
    }

    .info {
        font-size: 20;
        horizontal-align: center;
        vertical-align: center;
    }
</style>
