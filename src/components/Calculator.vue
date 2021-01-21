<template>
  <div class="calculator">
    <div class="display">{{ valueOnScreen || '0' }}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="sign" class="btn">+/-</div>
    <div @click="percentage" class="btn">%</div>
    <div @click="division" class="btn operator">/</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiplication" class="btn operator">*</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="substraction" class="btn operator">-</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="addition" class="btn operator">+</div>
    <div @click="append('0')" class="btn zero">0</div>
    <div @click="decimal" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',

  data(){
    return{
      valueOnScreen: '0',
      operator: null,
      stamp: null,
      clicked: false
    }
  },

  methods:{
    clear(){
      this.valueOnScreen = ''
      this.operator= null
      this.stamp= null
      this.clicked=false
    },

    sign(){
      this.valueOnScreen = (this.valueOnScreen.charAt(0) === '-') ?
          `${this.valueOnScreen.slice(1)}` : `-${this.valueOnScreen}`
    },

    percentage(){
      this.valueOnScreen = `${parseFloat(this.valueOnScreen)/100}`
    },

    append(payload){
      if (this.clicked){
        this.valueOnScreen = ''
        this.clicked = false
      }
      if (this.valueOnScreen === '0'){
        this.valueOnScreen = payload
      }else{
        this.valueOnScreen += payload
      }
    },

    decimal(){
      if (this.valueOnScreen.indexOf('.') === -1){
        this.append('.')
      }
    },

    changeState(){
      if (this.operator !== null)
        this.equal()
      this.stamp = this.valueOnScreen
      this.clicked = true
    },

    division(){
      this.changeState()
      this.operator = "divide"
    },

    multiplication(){
      this.changeState()
      this.operator = "times"
    },

    substraction(){
      this.changeState()
      this.operator = "minus"
    },

    addition(){
      this.changeState()
      this.operator = "add"
    },

    equal(){
      if (this.stamp !== null ){
        switch (this.operator){
          case "add":
            this.valueOnScreen = `${parseFloat(this.stamp) + parseFloat(this.valueOnScreen)}`
              break;
            case "minus":
              this.valueOnScreen = `${parseFloat(this.stamp) - parseFloat(this.valueOnScreen)}`
              break;
          case "times":
            this.valueOnScreen = `${parseFloat(this.stamp) * parseFloat(this.valueOnScreen)}`
            break;
          case "divide":
            this.valueOnScreen = `${parseFloat(this.stamp) / parseFloat(this.valueOnScreen)}`
            break;
        }
      }
    }
  }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

.calculator{
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  font-size: 40px;
  margin: auto;
}

.display{
  background-color: #333;
  grid-column: 1/5;
  color: white;
  padding: 15px;
  text-align: right;
}

.zero{
  grid-column: 1 / 3;
}

.btn{
  background-color: #eee;
  border: 1px solid #999;
  padding: 5px;
}

.btn:hover{
  background-color: #999999;
  color: #eeeeee;
}

.operator{
  background-color: orange;
  color: #fff;
}

.operator:hover{
  color: black;
  background-color: white;
}
</style>
