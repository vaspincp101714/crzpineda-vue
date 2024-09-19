<template>
  <div id="app">
    <h1 class="title">Melissa Yamileth Cruz Pineda</h1>
    <h2>Aplicacion de Calculadora</h2>
    <div class="calculator">
      <input type="text" class="result" :value="result" readonly>
      <div class="buttons">
        <button class="number" @click="handleClick('7')">7</button>
        <button class="number" @click="handleClick('8')">8</button>
        <button class="number" @click="handleClick('9')">9</button>
        <button class="operator" @click="handleOperatorClick('/')">/</button>

        <button class="number" @click="handleClick('4')">4</button>
        <button class="number" @click="handleClick('5')">5</button>
        <button class="number" @click="handleClick('6')">6</button>
        <button class="operator" @click="handleOperatorClick('*')">*</button>

        <button class="number" @click="handleClick('1')">1</button>
        <button class="number" @click="handleClick('2')">2</button>
        <button class="number" @click="handleClick('3')">3</button>
        <button class="operator" @click="handleOperatorClick('-')">-</button>

        <button class="number" @click="handleClick('0')">0</button>
        <button class="number" @click="handleClick('.')">.</button>
        <button class="number" @click="handleClick('00')">00</button>
        <button class="operator" @click="handleOperatorClick('+')">+</button>

        <button class="number" @click="handleClear()">C</button>
        <button class="number" @click="handleClearEntry()">CE</button>
        <button class="number" @click="calculate()">=</button>
      </div>
    </div>
  </div>
  <!--<router-view/>-->
</template>

<script>
export default{
  name: 'App',
  data(){
    return{
      result: '',
      calculated: false
    };
  },
  methods: {
    handleClick(value){
      if(this.calculated){
        this.result = value;
        this.calculated = false;
      }else{
        this.result += value;
      }
    },
    handleClear(){
      this.result =  '';
      this.calculated = false;
    },
    handleClearEntry(){
      if(this.result && this.result.lengh > 0){
        this.result = this.result.slice(0,-1);
        if(this.result.lengh === 0){
          this.handleClear();
        }
      }else{
        this.handleClear();
      }
    },
    handleOperatorClick(operator){
      if(/[+*/-]$/.test(this.result) ){
        this.result = this.result.slice(0,-1)+operator;
      }else{
        this.result += operator;
      }
      this.calculated = false;
    }, 
    calculate(){
      try{
        let evaluateResult = eval(this.result.replace(/(^|[^0-9])0+(\d+)/g, '$1$2'));
        if(evaluateResult === Infinity || evaluateResult === -Infinity){
          throw new Error('Division por cero');
        }
        this.result = Number.isFinite(evaluateResult) ? evaluateResult : 'Error';
      }catch(error){
        if(error.message ==  'Division por cero'){
          this.result =  'Error: Division por cero';
        }else{
          this.error =  'Error';
        }
      }
    }
  },
}
</script>

<style src="./calculadora.css">

</style>
