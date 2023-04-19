<template>
    <Page>
      <ActionBar>
        <NavigationButton text="Go back" android.systemIcon="ic_menu_back" @tap="goToHome" />
        <Label text="Конвертер массы"/>
      </ActionBar>
      <FlexboxLayout flexDirection="column">
        <FlexboxLayout flexDirection="column">
            <Label class="hynt" text="Введите величину:"/>
            <TextField v-model="textFieldValue" keyboardType="number" maxLength="15" class="textfield"/>
            <ListPicker :items="measure" v-model="selectedMeasure" class="selector"/>
        </FlexboxLayout>
        <FlexboxLayout flexDirection="column">
            <Label text="В других величинах: " class="output_label"/>
            <label :text="g" class="label"/>
            <label :text="kg" class="label"/>
            <label :text="centner" class="label"/>
            <label :text="t" class="label"/>
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
            measure: ["г", "кг", "ц", "т"],
            selectedMeasure: "",
            g: "",
            kg: "",
            centner: "",
            t: "",
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
                this.g = `Грамм: ${this.textFieldValue * 1}`;
                this.kg = `Килограмм: ${this.textFieldValue * 0.001}`;
                this.centner = `Центнеров: ${this.textFieldValue * 0.00001}`;
                this.t = `Тонн: ${this.textFieldValue * 0.000001}`;
            }
            switch (this.selectedMeasure) {
                case 0: //расчитываем из граммов
                    this.g = `Грамм: ${this.textFieldValue * 1}`;
                    this.kg = `Килограмм: ${this.textFieldValue * 0.001}`;
                    this.centner = `Центнеров: ${this.textFieldValue * 0.00001}`;
                    this.t = `Тонн: ${this.textFieldValue * 0.000001}`;
                    break;
                case 1: //Расчет из килограммов
                    this.g = `Грамм: ${this.textFieldValue * 1000}`;
                    this.kg = `Килограмм: ${this.textFieldValue * 1}`;
                    this.centner = `Центнеров: ${this.textFieldValue * 0.01}`;
                    this.t = `Тонн: ${this.textFieldValue * 0.001}`;
                    break;
                case 2: //Расчет из центнеров
                    this.g = `Грамм: ${this.textFieldValue * 100000}`;
                    this.kg = `Килограмм: ${this.textFieldValue * 100}`;
                    this.centner = `Центнеров: ${this.textFieldValue * 1}`;
                    this.t = `Тонн: ${this.textFieldValue * 0.1}`;
                    break;
                case 3: //Расчет из тонны
                    this.g = `Грамм: ${this.textFieldValue * 1000000}`;
                    this.kg = `Килограмм: ${this.textFieldValue * 1000}`;
                    this.centner = `Центнеров: ${this.textFieldValue * 10}`;
                    this.t = `Тонн: ${this.textFieldValue * 1}`;
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
