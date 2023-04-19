<template>
    <Page>
      <ActionBar>
        <NavigationButton text="Go back" android.systemIcon="ic_menu_back" @tap="goToHome" />
        <Label text="Конвертер температуры"/>
      </ActionBar>
      <FlexboxLayout flexDirection="column">
        <FlexboxLayout flexDirection="column">
            <Label class="hynt" text="Введите величину:"/>
            <TextField v-model="textFieldValue" keyboardType="number" maxLength="15" class="textfield"/>
            <ListPicker :items="measure" v-model="selectedMeasure" class="selector"/>
        </FlexboxLayout>
        <FlexboxLayout flexDirection="column">
            <Label text="В других величинах: " class="output_label"/>
            <label :text="c" class="label"/>
            <label :text="k" class="label"/>
            <label :text="f" class="label"/>
        </FlexboxLayout>
      </FlexboxLayout>
    </Page>
  </template>


<script>
import Home from './Home.vue'

  
    export default {
    data() {
        return {
            textFieldValue: "0",
            measure: ["Цельсия", "Кельвин", "Фаренгейт"],
            selectedMeasure: "",
            с:"",
            k:"",
            f:"",
        };
    },
    watch: {
        textFieldValue: function () {
            this.calculate();
        },
        selectedMeasure: function () {
            this.calculate();
        },
    },
    methods: {
        goToHome() {
            this.$navigateTo(Home);
        },
        calculate() {
            if (isNaN(this.selectedMeasure)) {
                this.c = `Цельсий: ${parseFloat(this.textFieldValue)*1}`;
                this.k = `Кельвин: ${parseFloat(this.textFieldValue)+273.15}`;
                this.f = `Фаренгейт: ${eval(parseFloat(this.textFieldValue)*1.8+32)}`;
            }
            if (this.textFieldValue == ''){
                this.c = `Цельсий: `;
                this.k = `Кельвин: `;
                this.f = `Фаренгейт: `;
            }
            switch (this.selectedMeasure) {
                case 0: //расчитываем из Цельсий
                    this.c = `Цельсий: ${parseFloat(this.textFieldValue)*1}`;
                    this.k = `Кельвин: ${parseFloat(this.textFieldValue)+273.15}`;
                    this.f = `Фаренгейт: ${eval(parseFloat(this.textFieldValue)*1.8+32)}`;
                    if (this.textFieldValue == ''){
                        this.c = `Цельсий: `;
                        this.k = `Кельвин: `;
                        this.f = `Фаренгейт: `;
                    }
                    break;
                case 1: //Расчет из Кельвинов
                    this.c = `Цельсий: ${parseFloat(this.textFieldValue)-273.15}`;
                    this.k = `Кельвин: ${parseFloat(this.textFieldValue)*1}`;
                    this.f = `Фаренгейт: ${eval((parseFloat(this.textFieldValue)-273.15)*1.8 + 32)}`;
                    if (this.textFieldValue == ''){
                        this.c = `Цельсий: `;
                        this.k = `Кельвин: `;
                        this.f = `Фаренгейт: `;
                    }
                    break;
                case 2: //Расчет из Фаренгейтов
                    this.c = `Цельсий: ${eval((parseFloat(this.textFieldValue)-32)*0.555555555)}`;
                    this.k = `Кельвин: ${eval(((parseFloat(this.textFieldValue)-32)*0.555555555)+273.15)}`;
                    this.f = `Фаренгейт: ${parseFloat(this.textFieldValue)*1}`;
                    if (this.textFieldValue == ''){
                        this.c = `Цельсий: `;
                        this.k = `Кельвин: `;
                        this.f = `Фаренгейт: `;
                     }
                    break;
            }
        },
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
