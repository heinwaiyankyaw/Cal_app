<template>
  <div class="container-fluid mt-5">
    <div class="container">
      <div class="text-center my-3">
        <h3>My Calculator</h3>
        <small class="fs-6 text-muted">Simple number can be calculated.</small>
      </div>
      <div class="card shadow-sm bg-gradient bg-secondary">
        <div class="card-body">
          <div class="row m-2">
            <div class="col bg-dark text-white d-flex justify-content-end rounded">
              <h4 class="mt-2">{{ calculatorValue || 0 }}</h4>
            </div>
          </div>
          <div class="row m-2">
            <div class="col-3" v-for="n in calculateElement" :key="n">
              <div class="btn btn-primary w-100 text-white p-2 mb-2" @click="action(n)">{{ n }}</div>
            </div>
          </div>
          <!-- <div class="row m-2">
            <div class="col">
              <button class="btn btn-primary w-100 text-white p-2">7</button>
            </div>
            <div class="col">
              <button class="btn btn-primary w-100 text-white p-2">8</button>
            </div>
            <div class="col">
              <button class="btn btn-primary w-100 text-white p-2">9</button>
            </div>
            <div class="col">
              <button class="btn btn-primary w-100 text-white p-2">/</button>
            </div>
          </div>-->
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data: () => ({
    calculatorValue:'',
    calculateElement: [7, 8, 9, '/', 4, 5, 6, '*', 1, 2, 3, '-', 'CE', 0, '+', 'En'],
    previouseCal : '',
    operator : null,
  }),
  methods :{
    action(n){
      if(!isNaN(n) || n === '.'){
        this.calculatorValue += n + '';
      }
      if(n === 'CE'){
        this.calculatorValue = '';
      }
      if(['/','*','-','+'].includes(n)){
        this.operator = n;
        this.previouseCal = this.calculatorValue;
        this.calculatorValue = '';
      }
      if(n === 'En'){
        this.calculatorValue = eval(
          this.previouseCal + this.operator + this.calculatorValue
        )
        this.previouseCal = '';
        this.operator = null;
      }
    }
  }
}
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Roboto+Mono&display=swap");

* {
  font-family: "Roboto Mono", monospace;
}
</style>
