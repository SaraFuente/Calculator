<template>
  <div class="container align-self-center border border-dark rounded bg-primary pb-3 ps-3 pe-3" style=" width:250px">
    <div class="border border-dark rounded bg-light mt-3" style="height:68px;">
      <h2 class="fst-normal p-3 text-end">{{operation}}</h2>
    </div>
    <div class="row mt-2 m-0">
      <button type="button" class="col-2 btn btn-outline-light ms-0" value="7" @click="setOperation($event.target.value)">7</button>
      <button type="button" class="col-2 btn btn-outline-light ms-2" value="8" @click="setOperation($event.target.value)">8</button>
      <button type="button" class="col-2 btn btn-outline-light ms-2" value="9" @click="setOperation($event.target.value)">9</button>
      <button type="button" class="col btn btn-outline-dark ms-2" value="/" @click="setOperation($event.target.value)">/</button>
    </div>
    <div class="row mt-2 m-0">
      <button type="button" class="col-2 btn btn-outline-light ms-0" value="4" @click="setOperation($event.target.value)">4</button>
      <button type="button" class="col-2 btn btn-outline-light ms-2" value="5" @click="setOperation($event.target.value)">5</button>
      <button type="button" class="col-2 btn btn-outline-light ms-2" value="6" @click="setOperation($event.target.value)">6</button>
      <button type="button" class="col btn btn-outline-dark ms-2" value="*" @click="setOperation($event.target.value)">x</button>
    </div>
    <div class="row mt-2 m-0">
      <button type="button" class="col-2 btn btn-outline-light ms-0" value="1" @click="setOperation($event.target.value)">1</button>
      <button type="button" class="col-2 btn btn-outline-light ms-2" value="2" @click="setOperation($event.target.value)">2</button>
      <button type="button" class="col-2 btn btn-outline-light ms-2" value="3" @click="setOperation($event.target.value)">3</button>
      <button type="button" class="col btn btn-outline-dark ms-2" value="-" @click="setOperation($event.target.value)">-</button>
    </div>
    <div class="row mt-2 m-0">
      <button type="button" class="col-2 btn btn-outline-light ms-0" value="0" @click="setOperation($event.target.value)">0</button>
      <button type="button" class="col-2 btn btn-outline-light ms-2" @click="reset()">C</button>
      <button type="button" class="col-2 btn btn-outline-info ms-2" @click="calculate()">=</button>
      <button type="button" class="col btn btn-outline-dark ms-2" value="+" @click="setOperation($event.target.value)">+</button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorTask',
  data() {
    return {
      operation: ''
    }
  },
  methods:{
    reset(){
      this.operation= ''
    },
    setOperation(value){
      if((this.operation + value).length > 11){
        alert('No caben más cifras')
      }else if([...this.operation + value].filter(op=>this.isOp(op)).length > 1){
        this.calculate()
      }else{
        this.operation+=value
      }
      console.log(this.operation)
    },
    isOp(str){
      const operator = /[/*--+]/;
      return operator.test(str);
    },
    calculate(){
      let numbers= this.operation.split(/[/*--+]/).map(Number)
      if(this.operation.indexOf('+') !== -1){
        this.operation = numbers[0] + numbers[1]
      }else if(this.operation.indexOf('-') !== -1){
        this.operation = numbers[0] - numbers[1]
      }
      console.log('calcula', this.operation)

    }
  }
}
</script>

<style scoped>

</style>
