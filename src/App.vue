<template>
  <div id="app">
    <div class="container">
      <div class="row">
        <div class="col current "> {{current}} </div>
        <div class="w-100"></div>
        <div @click="clear" class="col-sm border btn border-dark other">C</div>
        <div @click="sign" class="col-sm border btn border-dark other">+ / -</div>
        <div @click="percent" class="col-sm border btn border-dark other">%</div>
        <div @click="divide" class="col-sm border btn border-dark operator">÷</div>
        <div class="w-100"></div>
        <div @click="append(7)" class="col-sm border btn border-dark">7</div>
        <div @click="append(8)" class="col-sm border btn border-dark">8</div>
        <div @click="append(9)" class="col-sm border btn border-dark">9</div>
        <div @click="multiply" class="col-sm border btn border-dark operator">x</div>
        <div class="w-100"></div>
        <div @click="append(4)" class="col-sm border btn border-dark">4</div>
        <div @click="append(5)" class="col-sm border btn border-dark">5</div>
        <div @click="append(6)" class="col-sm border btn border-dark">6</div>
        <div @click="minus" class="col-sm border btn border-dark operator">-</div>
        <div class="w-100"></div>
        <div @click="append(1)" class="col-sm border btn border-dark">1</div>
        <div @click="append(2)" class="col-sm border btn border-dark">2</div>
        <div @click="append(3)" class="col-sm border btn border-dark">3</div>
        <div @click="sum" class="col-sm border btn border-dark operator">+</div>
        <div class="w-100"></div>
        <div @click="append(0)" class="col-sm-6 border btn border-dark"> 0 </div>
        <div @click="dot" class="col-sm border btn border-dark">.</div>
        <div @click="equal" class="col-sm border btn border-dark operator">=</div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      current : "",
      previous : null,
      operatorClicked : false,
      operator : null,
    }
  },
  methods : {
    append(number) {
        if(this.operatorClicked === true) {
          this.current = "";
          this.operatorClicked = false;
        }
        this.current =  `${this.current}${number}`
    },
    equal() {
      this.current = this.operator(Number(this.previous), Number(this.current));
      this.previous = null;
      this.operatorClicked = true;
    },
    clear() {
      this.current = "";
    },
    sign() {
      this.current = this.current - this.current * 2 ;
    },
    percent() {
      this.current = this.current / 100
    },
    divide() {
      this.operator = (a, b) => a / b ;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    multiply() {
      this.operator = (a, b) => a * b ;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    minus() {
      this.operator = (a, b) => a - b ;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    sum() {
      this.operator = (a, b) => a + b ;
      this.previous = this.current;
      this.operatorClicked = true;
    },
    dot() {
      if(this.current != ""){
        this.append(".")
      }
    }
  }
}
</script>

<style lang="scss">
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.row{
  width: 400px;
  height: 125px;
}
.w-100{
  height: 0px;
}
.operator{
  background-color: orange;
}
.other{
  background-color: silver;
}
.current{
  background-color: #333;
  color: white;
  height: 25px;
  text-align: right;
}
.btn{
   cursor:pointer
}
.btn:active{
   transform: scale(0.95);
}
</style>
