<template>
  <div class="">
    <input type="number" v-model.number="num1" placeholder="num1" />
    {{ symbol }}
    <input type="number" v-model.number="num2" placeholder="num2" />
    = {{ result }}
    <div class="buttons">
      <button @click="sum">+</button>
      <button @click="diff">-</button>
      <button @click="mult">*</button>
      <button @click="div">/</button>
      <br>
      <button @click="intdiv">Целочисленное деление</button>
      <button @click="exponent">Возведение в степень</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calc",
  data() {
    return {
      num1: 0,
      symbol: "?",
      num2: 0,
      result: 0,
    };
  },
  methods: {
    sum() {
      this.result = this.num1 + this.num2;
      this.symbol = " + ";
    },
    diff() {
      this.result = this.num1 - this.num2;
      this.symbol = " - ";
    },
    mult() {
      this.result = this.num1 * this.num2;
      this.symbol = " * ";
    },
    div() {
      if (this.num2 !== 0){
      this.result = this.num1 / this.num2;
      this.symbol = " / ";}
      else this.result = "На ноль делить нельзя"
    },
    intdiv(){
      if (this.num2 == 0){
        this.result = "На ноль делить нельзя"
      } else{
        if (this.num1/this.num2 >= 0){
        this.result = Math.floor(this.num1/this.num2)
        } else this.result = Math.ceil(this.num1/this.num2)
      }
    },
    exponent() {
      this.result = Math.pow(this.num1, this.num2)
    },
  },
};
</script>

<style lang="sass" scoped>
</style>