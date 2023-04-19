<template>
    <Page>
      <ActionBar>
        <NavigationButton text="Go back" android.systemIcon="ic_menu_back" @tap="goToHome" />
        <Label text="Конвертер скорости"/>
      </ActionBar>
      <FlexboxLayout flexDirection="column">
        <FlexboxLayout flexDirection="column">
            <Label class="hynt" text="Введите величину:"/>
            <TextField v-model="textFieldValue" keyboardType="number" maxLength="15" class="textfield"/>
            <ListPicker :items="measure" v-model="selectedMeasure" class="selector"/>
        </FlexboxLayout>
        <FlexboxLayout flexDirection="column">
            <Label text="В других величинах: " class="output_label"/>
            <label :text="kmH" class="label"/>
            <label :text="mS" class="label"/>
            <label :text="mlH" class="label"/>
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
        measure: ["Км/ч","М/c", "Миль/ч"],
        selectedMeasure: "",
        kmH: "",
        mS: "",
        mlH: "",
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
            this.kmH = `Километры/час: ${this.textFieldValue * 1}`;
            this.mS = `Метр/секунда: ${this.textFieldValue / 3.6}`;
            this.mlH = `Миля/час: ${this.textFieldValue / 1.609}`;
        }
        switch (this.selectedMeasure) {
            case 0: //расчитываем из км\ч
                this.kmH = `Километры/час: ${this.textFieldValue * 1}`;
                this.mS = `Метр/секунда: ${this.textFieldValue / 3.6}`;
                this.mlH = `Миля/час: ${this.textFieldValue / 1.609}`;
                break;
            case 1: //Расчет из м\с
                this.kmH = `Километры/час: ${this.textFieldValue * 3.6}`;
                this.mS = `Метр/секунда: ${this.textFieldValue * 1}`;
                this.mlH = `Миля/час: ${this.textFieldValue * 2.237}`;
                break;
            case 2: //Расчет из миль\ч
                this.kmH = `Километры/час: ${this.textFieldValue * 1.609}`;
                this.mS = `Метр/секунда: ${this.textFieldValue / 2.237}`;
                this.mlH = `Миля/час: ${this.textFieldValue * 1}`;
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
