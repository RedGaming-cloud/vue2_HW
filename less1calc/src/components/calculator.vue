<template>
<div class="start">
  <div class="inputs">
    <input type="number" id="operand1" v-model.number="op1">
    <input type="number" id="operand2" v-model.number="op2">
    = {{ result }}    
  </div>
  <div class="operators">
    <button class="button" @click="calculate(operator)" v-for="operator of operators" :key="operator">{{ operator }}</button>
  </div>
  <div class="check">
    <input type="checkbox" id="buttonshow" v-model="isShow">
    <label class="button-show" for="buttonshow" >Показать экранную клавиатуру</label>
  </div>
  <div class="numpad" v-if="isShow">
      <button class="button-numpad" v-for="number of buttonsNumber" :key="number" @click="addNumber(number)">{{ number }}</button>
      <button class="button-numpad" @click="backspace1()">Backspace</button>
  </div>  
  <div class="radio">
    <input type="radio" name="opselector" id="operand1" :value="op1" v-model="op1" checked>
    <label for="op1">Оператор 1</label>
    <input type="radio" name="opselector" id="operand2" :value="op2" v-model="op2" >
    <label for="op2">Оператор 2</label>
  </div>
</div>
</template>

<script>
export default {
  name: "Calculator",

  data: () => ({
    op1: 0,
    op2: 0,
    result: 0,
    isShow: true,  
    operators: ["+", "-", "/", "*", "целочисленное деление", "возведение в степень"],
    buttonsNumber: ["1", "2", "3", "4", "5", "6", "7", "8", "9", "0"],
    symbol: null,
  }),

  methods: {    
    add() {
      const {op1, op2} = this;
      this.result = parseInt(op1) + op2;
      this.symbol = "+"     
    },
    substract() {
      const {op1, op2} = this;
      this.result = op1 - op2;
      this.symbol = "-"
    },
    mult() {
      const {op1, op2} = this;
      this.result = op1 * op2;
      this.symbol = "*"
    },
    div() {
      if (this.op2 !== 0){
      const {op1, op2} = this;
      this.result = op1 / op2;
      this.symbol = " / ";}
      else this.result = "На ноль делить нельзя"
    },
    intdiv(){
      if (this.op2 == 0){
        this.result = "На ноль делить нельзя"
      } else{
        if (this.op1/this.op2 >= 0){
        this.result = Math.floor(this.op1/this.op2)
        } else this.result = Math.ceil(this.op1/this.op2)
      }
    },
    exponent() {
      this.result = Math.pow(this.op1, this.op2)
    },
    calculate(operation){
      switch(operation){
        case '+': this.add(); break;
        case '-': this.substract(); break;
        case '*': this.mult(); break;
        case '/': this.div(); break;
        case 'целочисленное деление': this.intdiv(); break;
        case 'возведение в степень': this.exponent(); break;
      }
    },

    addNumber(number){
      if (document.getElementsById('operand1').checked) {
        this.addNumber1(number);
        this.backspace1();
      } else{
        this.addNumber2(number);
        this.backspace2;
      }
    },
    backspace1(){
      if(this.op1.toString().length > 1){
        this.op1 = this.op1.toString().slice(0, -1);
        parseInt(this.op1);
      } else this.op1 = 0;
    },
    addNumber1(number) {
    if(this.op1 !== 0){
        this.op1 = parseInt(this.op1 + number);
      } else this.op1 = number;
    },
    backspace2(){
      if(this.op2.toString().length > 1){
        this.op2 = this.op2.toString().slice(0, -1);
        parseInt(this.op2);
      } else this.op2 = 0;
    },
    addNumber2(number) {
    if(this.op2 !== 0){
        this.op2 = parseInt(this.op2 + number);
      } else this.op2 = number;
    },    
  },  
}
</script>

<style lang="css">
  .inputs{
    display: flex;
    justify-content: center;
    gap: 10px;
    margin-bottom: 20px;
  };  
</style>
  
