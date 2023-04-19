<template>
    <Page>
      <ActionBar>
        <NavigationButton text="Go back" android.systemIcon="ic_menu_back" @tap="goToHome" />
        <Label text="Конвертер валют"/>
      </ActionBar>
      <FlexboxLayout flexDirection="column">
        <FlexboxLayout flexDirection="column">
            <Label class="hynt" text="Введите величину:"/>
            <TextField v-model="textFieldValue" keyboardType="number" maxLength="15" class="textfield"/>
            <ListPicker :items="measure" v-model="selectedMeasure" class="selector"/>
        </FlexboxLayout>
        <FlexboxLayout flexDirection="column">
            <Label text="В других величинах: " class="output_label"/>
            <label :text="ru" class="label"/>
            <label :text="dl" class="label"/>
            <label :text="eur" class="label"/>
            <label :text="yen" class="label"/>
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
        measure: ["Рубль", "Доллар", "Евро", "Йена"],
        selectedMeasure: "",
        ru: "",
        dl: "",
        eur: "",
        yen: "",
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
            this.ru = `Рубль: ${this.textFieldValue * 1}`;
            this.dl = `Доллар: ${this.textFieldValue / 81.65}`;
            this.eur = `Евро: ${this.textFieldValue / 89.37}`;
            this.yen = `Йена: ${this.textFieldValue / 1.65}`;
        }
        switch (this.selectedMeasure) {
            case 0: //расчитываем из рубля
                this.ru = `Рубль: ${this.textFieldValue * 1}`;
                this.dl = `Доллар: ${this.textFieldValue / 81.65}`;
                this.eur = `Евро: ${this.textFieldValue / 89.37}`;
                this.yen = `Йена: ${this.textFieldValue / 1.65}`;
                break;
            case 1: //Расчет из доллара
                this.ru = `Рубль: ${this.textFieldValue * 81.65}`;
                this.dl = `Доллар: ${this.textFieldValue * 1}`;
                this.eur = `Евро: ${this.textFieldValue / 0.91}`;
                this.yen = `Йена: ${this.textFieldValue * 134.67}`;
                break;
            case 2: //Расчет из евро
                this.ru = `Рубль: ${this.textFieldValue * 89.37}`;
                this.dl = `Доллар: ${this.textFieldValue / 1.09}`;
                this.eur = `Евро: ${this.textFieldValue * 1}`;
                this.yen = `Йена: ${this.textFieldValue * 147.66}`;
                break;
            case 3: //Расчет из йены
                this.ru = `Рубль: ${this.textFieldValue / 1.65}`;
                this.dl = `Доллар: ${this.textFieldValue / 134.67}`;
                this.eur = `Евро: ${this.textFieldValue / 147.66}`;
                this.yen = `Йена: ${this.textFieldValue * 1}`;
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
