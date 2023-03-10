<template>
  <div id="app">

    <input type="text" v-model="result">

    <div>
      <div class="calculator-row">
        <div @click="clickNum(7)">7</div>
        <div @click="clickNum(8)">8</div>
        <div @click="clickNum(9)">9</div>
        <div @click="clickNum('/')">/</div>
      </div>
    </div>
    <div>
      <div class="calculator-row">
        <div @click="clickNum(4)">4</div>
        <div @click="clickNum(5)">5</div>
        <div @click="clickNum(6)">6</div>
        <div @click="clickNum('*')">*</div>
      </div>
    </div>
    <div>
      <div class="calculator-row">
        <div @click="clickNum(1)">1</div>
        <div @click="clickNum(2)">2</div>
        <div @click="clickNum(3)">3</div>
        <div @click="clickNum('-')">-</div>
      </div>
    </div>
    <div>
      <div class="calculator-row">
        <div @click="clickNum(0)">0</div>
        <div></div>
        <div class="result" @click="getResult">=</div>
        <div @click="clickNum('+')">+</div>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'App',

  data(){
    return{
      result: 0,
      oneSet: '', // 1: num, 2: symbol, 3: num
      twoSet: '',
      threeSet: '',
      toggleStatue: []
    }
  },
  methods:{
    clickNum(num){
      let isSymbol = isNaN(num);
      console.log(isSymbol);
      if(isSymbol === false && this.toggleStatue[0] !== true){
        this.oneSet += num;
        this.result = this.oneSet;
      }
      if(isSymbol === true){
        this.twoSet += num;
        this.toggleStatue.push(true);
        console.log(this.toggleStatue[0]);
      }
      if(isSymbol === false && this.toggleStatue[0] === true){
        this.threeSet += num;
        console.log(this.toggleStatue);
        this.result = this.threeSet;
      }
      console.log(this.oneSet);
      console.log(this.threeSet);
    },
    getResult(){
      console.log("getReult");
      console.log(this.oneSet);
      console.log(this.threeSet);
      switch(this.twoSet[0]){
        case '/':
        this.result = this.oneSet / this.threeSet;
        break;
        case '*':
        this.result = this.oneSet * this.threeSet;
        break;
        case '+':
        this.result = Number(this.oneSet) + Number(this.threeSet);
        break;
        case '-':
        this.result = this.oneSet - this.threeSet;
        break;
      }
      this.oneSet = '';
      this.twoSet = '';
      this.threeSet = '';
      this.toggleStatue = [];
    }
  }

}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.calculator-row{
  display: flex;
}

.calculator-row div {
  background-color: #e3e3e3; 
  width: 40px; 
  height: 30px;
  line-height: 30px;
  margin: 5px;  
  padding: 5px;
  border-radius: 10px;
}

.calculator-row div:nth-child(4){
  background-color: #aaaaaa;
}

.result{
  background-color: aqua !important;
}

.calculator-row div:hover,
.result:hover{
  cursor: pointer;
  background-color: lightcoral !important;
}

input{
  width: 200px;
  height: 20px;
  margin: 0px 0px 20px 0px;
  text-align:right;
  font-size: 20px;
  border: 1px solid #bbbbbb;
  border-radius: 20px;
  padding: 10px;
}

</style>
