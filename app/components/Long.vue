<template>
    <Page>
      <ActionBar>
        <NavigationButton text="Go back" android.systemIcon="ic_menu_back" @tap="goToHome" />
        <Label text="Конвертер длинн"/>
      </ActionBar>
      <FlexboxLayout flexDirection="column">
        <FlexboxLayout flexDirection="column">
            <Label class="hynt" text="Введите величину:"/>
            <TextField v-model="textFieldValue" keyboardType="number" maxLength="15" class="textfield"/>
            <ListPicker :items="measure" v-model="selectedMeasure" class="selector"/>
        </FlexboxLayout>
        <FlexboxLayout flexDirection="column">
            <Label text="В других величинах: " class="output_label"/>
            <label :text="km" class="label"/>
            <label :text="m" class="label"/>
            <label :text="sm" class="label"/>
            <label :text="mm" class="label" />
            <label :text="fut" class="label"/>
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
        measure: ["Километр", "Метр", "Сантиметр", "Милиметр", "Фут"],
        selectedMeasure: "",
        km: "",
        m: "",
        sm: "",
        mm: "",
        fut: "",
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
            this.km = `Километр: ${this.textFieldValue * 1}`;
            this.m = `Метр: ${this.textFieldValue * 1000}`;
            this.sm = `Сантиметр: ${this.textFieldValue * 100000}`;
            this.mm = `Милиметр: ${this.textFieldValue * 1000000}`;
            this.fut = `Фут: ${this.textFieldValue * 3281}`;
        }
        switch (this.selectedMeasure) {
            case 0: //расчитываем из километров
                this.km = `Километр: ${this.textFieldValue * 1}`;
                this.m = `Метр: ${this.textFieldValue * 1000}`;
                this.sm = `Сантиметр: ${this.textFieldValue * 100000}`;
                this.mm = `Милиметр: ${this.textFieldValue * 1000000}`;
                this.fut = `Фут: ${this.textFieldValue * 3281}`;
                break;
            case 1: //Расчет из метров
                this.km = `Километр: ${this.textFieldValue / 1000}`;
                this.m = `Метр: ${this.textFieldValue * 1}`;
                this.sm = `Сантиметр: ${this.textFieldValue * 100}`;
                this.mm = `Милиметр: ${this.textFieldValue * 1000}`;
                this.fut = `Фут: ${this.textFieldValue * 3.281}`;
                break;
            case 2: //Расчет из сантиметров
                this.km = `Километр: ${this.textFieldValue / 100000}`;
                this.m = `Метр: ${this.textFieldValue / 100}`;
                this.sm = `Сантиметр: ${this.textFieldValue * 1}`;
                this.mm = `Милиметр: ${this.textFieldValue * 10}`;
                this.fut = `Фут: ${this.textFieldValue / 30.48}`;
                break;
            case 3: //Расчет из милиметров
                this.km = `Километр: ${this.textFieldValue / 1000000}`;
                this.m = `Метр: ${this.textFieldValue / 1000}`;
                this.sm = `Сантиметр: ${this.textFieldValue / 10}`;
                this.mm = `Милиметр: ${this.textFieldValue * 1}`;
                this.fut = `Фут: ${this.textFieldValue / 304.9}`;
                break;
            case 4: //расчет их футов
                this.km = `Километр: ${this.textFieldValue / 3281}`;
                this.m = `Метр: ${this.textFieldValue / 3.281}`;
                this.sm = `Сантиметр: ${this.textFieldValue * 30.48}`;
                this.mm = `Милиметр: ${this.textFieldValue * 304.8}`;
                this.fut = `Фут: ${this.textFieldValue * 1}`;
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
