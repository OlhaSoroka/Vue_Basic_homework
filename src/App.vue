<template>
  <div id="app">
    <div class="calc-container">
      <div class="allowed-operators">Allowed operators:{{allowedOperatorsList.join(", ")}}</div>
      <div class="inputs-container">
        <InputComponent @onInputChange="firstValueHandler"></InputComponent>
        <InputComponent @onInputChange="operatorHandler"></InputComponent>
        <InputComponent @onInputChange="secondValueHandler"></InputComponent>
      </div>
      <div class="inputs-container show" >
        <div>
          <span v-if='showFirstValueError' class="incorrect">Incorrect number</span>
          <span v-else class="correct">{{firstNumber}}</span>
        </div>
        <div>
          <span v-if='showOperatorError' class="incorrect">Incorrect operator</span>
         <span v-else class="correct">{{operator}}</span>

          </div>
        <div>
         <span v-if='showSecondValueError' class="incorrect">Incorrect number</span>
         <span v-else class="correct">{{secondNumber}}</span>

        </div>
      </div>
      <h2>Result:{{showFirstValueError||showSecondValueError||showOperatorError ?
        ' fix error please ':result }}</h2>
    </div>

  </div>
</template>

<script>
import InputComponent from './components/InputComponent.vue';

export default {
  name: 'App',
  components: {
    InputComponent,
  },
  data() {
    return {
      firstNumber: 0,
      secondNumber: 0,
      operator: '+',
      showFirstValueError: false,
      showSecondValueError: false,
      showOperatorError: false,
      allowedOperatorsList: ['+', '-', '*', '/', '**'],
    };
  },
  methods: {
    firstValueHandler(event) {
      if (+event) {
        this.firstNumber = +event;
        this.showFirstValueError = false;
      } else {
        this.showFirstValueError = true;
      }
    },
    secondValueHandler(event) {
      if (+event) {
        this.secondNumber = +event;
        this.showSecondValueError = false;
      } else {
        this.showSecondValueError = true;
      }

      this.secondNumber = +event;
    },
    operatorHandler(event) {
      if (event && this.allowedOperatorsList.includes(event)) {
        this.showOperatorError = false;
        this.operator = event;
      } else {
        this.showOperatorError = true;
      }
    },
  },
  computed: {
    result() {
      // eslint-disable-next-line no-eval
      return eval(`${this.firstNumber} ${this.operator} ${this.secondNumber}`);
    },
  },
};
</script>

<style lang="scss">
*{
font-family: 'Roboto', sans-serif;
}
.calc-container{
  background: silver;
  width: 800px;
  margin: 50px auto;
  border-radius: 20px;
}
.inputs-container{
  display: flex;
  justify-content: space-around;
  padding: 30px 10px;
  &.show{
    font-size: 2rem;
    font-weight: bold;
  }
}
h2{
  text-align: center;
  color: green;
  font-size: 2rem;
  padding-bottom: 20px;
}
input{
  widows: 30px;
  height: 30px;
  border-radius: 10px;
}
.allowed-operators{
  padding-top: 20px;
  text-align: center;
  color: tomato;
  font-size: 1.5rem;
  font-weight: bold;
}
.incorrect{
  text-align: center;
  color: tomato;
  font-size: 1.5rem;
  font-weight: bold;
}
.correct{
  text-align: center;
  color: green;
  font-size: 2rem;
  font-weight: bold;
}
</style>
