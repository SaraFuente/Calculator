<template>
  <h1 class="mb-2 text-center">Sara Fuente</h1>
  <h5 class="mb-4 text-center">Calculadora con Vue.js y Bootstrap</h5>
  <div class="d-flex ms-4 me-4 ps-2 pe-2">
    <div class="text-start align-self-end mx-auto p-3">
      <p>Características:</p>
      <ul>
        <li>Solo se empieza a escribir por número</li>
        <li>No escribir 2 operadores seguidos</li>
        <li>No más de {{charLimit}} caractéres por operación</li>
        <li>Solo una operación simultánamente</li>
        <li class="mb-5">Resultado redondeado a 2 decimales</li>
      </ul>
    </div>
    <div class="container  border border-dark rounded bg-primary pb-3 ps-3 pe-3" style=" width:250px; box-shadow:8px 8px 10px 2px black;">
      <div class="border border-dark rounded bg-light mt-3" style="height:68px; box-shadow: inset 4px 4px 10px -2px black;">
        <h2 class="fst-normal p-3 text-end">{{operation}}</h2>
      </div>
      <div class="row mt-2 m-0">
        <button type="button" class="col-2 btn btn-outline-light ms-0" value="7" @click="checkOperation($event.target.value)">7</button>
        <button type="button" class="col-2 btn btn-outline-light ms-2" value="8" @click="checkOperation($event.target.value)">8</button>
        <button type="button" class="col-2 btn btn-outline-light ms-2" value="9" @click="checkOperation($event.target.value)">9</button>
        <button type="button" class="col-2 btn btn-outline-light ms-2" @click="reset()">C</button>
        <button type="button" class="col-2 btn btn-outline-light ms-2 p-0" @click="del()">DEL</button>
      </div>
      <div class="row mt-2 m-0">
        <button type="button" class="col-2 btn btn-outline-light ms-0" value="4" @click="checkOperation($event.target.value)">4</button>
        <button type="button" class="col-2 btn btn-outline-light ms-2" value="5" @click="checkOperation($event.target.value)">5</button>
        <button type="button" class="col-2 btn btn-outline-light ms-2" value="6" @click="checkOperation($event.target.value)">6</button>
        <button type="button" class="col-2 btn btn-outline-dark ms-2" value="*" @click="checkOperation($event.target.value)">x</button>
        <button type="button" class="col-2 btn btn-outline-dark ms-2" value="/" @click="checkOperation($event.target.value)">/</button>
      </div>
      <div class="row mt-2 m-0">
        <button type="button" class="col-2 btn btn-outline-light ms-0" value="1" @click="checkOperation($event.target.value)">1</button>
        <button type="button" class="col-2 btn btn-outline-light ms-2" value="2" @click="checkOperation($event.target.value)">2</button>
        <button type="button" class="col-2 btn btn-outline-light ms-2" value="3" @click="checkOperation($event.target.value)">3</button>
        <button type="button" class="col-2 btn btn-outline-dark ms-2" value="+" @click="checkOperation($event.target.value)">+</button>
        <button type="button" class="col-2 btn btn-outline-dark ms-2" value="-" @click="checkOperation($event.target.value)">-</button>
      </div>
      <div class="row mt-2 m-0">
        <button type="button" class="col btn btn-outline-light ms-0" value="0" @click="checkOperation($event.target.value)">0</button>
        <button type="button" class="col-2 btn btn-outline-light pe-2 ms-2" value="." @click="checkOperation($event.target.value)">.</button>
        <button type="button" class="col btn btn-info ms-2" @click="compute()">=</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorTask',
  data() {
    return {
      operation: '',
      charLimit: '11'
    }
  },
  methods:{
    reset(){
      this.operation= ''
    },
    del(){
      this.operation= this.operation.slice(0, -1)
    },
    checkOperation(value){
      if(!this.isNumber((this.operation + value)[0])){
      // solo se puede empezar por un número
        alert('Escribe un número')
        return
      }
      if(this.isRepeated(this.operation + value)){
      // No pulsar dos operadores seguidos ni 2 comas
        alert('No pulsar 2 operadores seguidos')
        return
      }
      if((this.operation + value).length > this.charLimit){
      // charLimit máximo de caractéres
        alert('No más de '+this.charLimit+' caractéres')
      }else if([...this.operation + value].filter(op=>this.isOp(op)).length > 1){
      // una operación simultánea
        this.compute()
      }else{
        this.operation+=value
      }
    },
    isNumber(str){
      return /[0-9]/.test(str)
    },
    isRepeated(str){
      const lastCharIdx = str.length -1
      if(lastCharIdx>0 && /[./*--+]/.test(str[lastCharIdx]) && /[./*--+]/.test(str[lastCharIdx-1])){
        return true
      }
      return false
    },
    isOp(str){
      return /[/*--+]/.test(str);
    },
    compute(){
      let numbers= this.operation.split(/[/*--+]/).map(Number)
      if(this.operation.indexOf('+') !== -1){
        this.operation = Math.round((numbers[0] + numbers[1])*100)/100
      }else if(this.operation.indexOf('-') !== -1){
        this.operation = Math.round((numbers[0] - numbers[1])*100)/100
      }else if(this.operation.indexOf('*') !== -1){
        this.operation = Math.round((numbers[0] * numbers[1])*100)/100
      }else if(this.operation.indexOf('/') !== -1){
        this.operation = Math.round((numbers[0] / numbers[1])*100)/100
      }
    }
  }
}
</script>

<style scoped>
  button {
    box-shadow: 3px 3px 5px 1px black;
  }
</style>
