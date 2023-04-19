<template>
    <Page>
      <ActionBar>
        <NavigationButton text="Go back" android.systemIcon="ic_menu_back" @tap="goToHome" />
        <Label text="Конвертер времени"/>
      </ActionBar>
      <FlexboxLayout flexDirection="column">
        <FlexboxLayout flexDirection="column">
            <Label class="hynt" text="Введите величину:"/>
            <TextField v-model="textFieldValue" keyboardType="number" maxLength="15" class="textfield"/>
            <ListPicker :items="measure" v-model="selectedMeasure" class="selector"/>
        </FlexboxLayout>
        <FlexboxLayout flexDirection="column">
            <Label text="В других величинах: " class="output_label"/>
            <label :text="hour" class="label"/>
            <label :text="minute" class="label"/>
            <label :text="sec" class="label"/>
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
        measure: ["Час", "Минута", "Секунда"],
        selectedMeasure: "",
        hour: "",
        minute: "",
        sec: "",
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
            this.hour = `Час: ${this.textFieldValue * 1}`;
            this.minute = `Минута: ${this.textFieldValue *60}`;
            this.sec = `Секунда: ${this.textFieldValue * 3600}`;
        }
        switch (this.selectedMeasure) {
            case 0: //расчитываем из часа
                this.hour = `Час: ${this.textFieldValue * 1}`;
                this.minute = `Минута: ${this.textFieldValue *60}`;
                this.sec = `Секунда: ${this.textFieldValue * 3600}`;
                break;
            case 1: //Расчет из минуты
                this.hour = `Час: ${this.textFieldValue / 60}`;
                this.minute = `Минута: ${this.textFieldValue *1}`;
                this.sec = `Секунда: ${this.textFieldValue * 60}`;
                break;
            case 2: //Расчет из секунды
                this.hour = `Час: ${this.textFieldValue / 3600}`;
                this.minute = `Минута: ${this.textFieldValue / 60}`;
                this.sec = `Секунда: ${this.textFieldValue * 1}`;
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
