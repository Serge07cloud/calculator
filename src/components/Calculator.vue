<template>
  <div class="row-cols-4 w-50 m-auto">
    <h1 class="col-12">{{ title }}</h1>
    <div class="col-12 bg-dark text-white text-right p-3 h3">{{ valueOnScreen || '0' }}</div>
    <div class="w-100"></div>
    <div @click="clear" class="col btn btn-warning">C</div>
    <div @click="sign"  class="col btn btn-light">+/-</div>
    <div @click="percentage" class="col btn btn-light">%</div>
    <div @click="append('/')" class="col btn btn-light">/</div>
    <div class="w-100"></div>
    <div @click="append('7')" class="col btn btn-light">7</div>
    <div @click="append('8')" class="col btn btn-light">8</div>
    <div @click="append('9')" class="col btn btn-light">9</div>
    <div @click="append('*')" class="col btn btn-light">*</div>
    <div class="w-100"></div>
    <div @click="append('4')" class="col btn btn-light">4</div>
    <div @click="append('5')" class="col btn btn-light">5</div>
    <div @click="append('6')" class="col btn btn-light">6</div>
    <div @click="append('-')" class="col btn btn-light">-</div>
    <div class="w-100"></div>
    <div @click="append('1')" class="col btn btn-light">1</div>
    <div @click="append('2')" class="col btn btn-light">2</div>
    <div @click="append('3')" class="col btn btn-light">3</div>
    <div @click="append('+')" class="col btn btn-light">+</div>
    <div class="w-100"></div>
    <div @click="append('0')" class="col-6 btn btn-light">0</div>
    <div @click="decimal" class="col btn btn-light">.</div>
    <div @click="equal" class="col btn btn-success">=</div>
  </div>
</template>

<script>
export default {
  name: 'Calculator',

  data(){
    return{
      valueOnScreen: '0'
    }
  },

  props:{
    title:{
      type: String,
      required : true
    }
  },

  methods:{
    clear(){
      this.valueOnScreen = ''
    },

    sign(){
      this.valueOnScreen = (this.valueOnScreen.charAt(0) === '-') ?
          `${this.valueOnScreen.slice(1)}` : `-${this.valueOnScreen}`
    },

    percentage(){
      this.valueOnScreen = `${parseFloat(this.valueOnScreen)/100}`
    },

    append(payload){
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

    equal(){
      this.valueOnScreen = `${eval(this.valueOnScreen)}`
    }
  }

  }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.btn{
  font-size: 1.4em;
}
</style>
