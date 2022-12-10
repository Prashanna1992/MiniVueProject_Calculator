<template>
  <div class="p-3 col-md-4 mx-auto my-5 bg-dark text-white">
   
    <!-- Calculator Resule -->
    <div class="w-full rounded m-1 p-3 text-end lead font-weight-bold text-white bg-vue-dark mb-3">
      {{calculatorValue || 0}}
    </div>
    <div class="row g-0">
      <div class="col-3" v-for="(element, key) in calculatorElements" :key="key" >
        <div class="lead text-white text-center py-3 m-1 bg-vue-dark rounded hover-class" 
          :class="{'bg-vue-green' : ['C', '*','/','-','+','%','='].includes(element)}" @click="action(element)">
          {{element}}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CalculatorVue',
  props: {
    msg: String
  },
  methods:{
    action(n){
      if(!isNaN(n) || n ==='.'){
        this.calculatorValue += n +'';
      }
      else if(n === 'C'){
        this.calculatorValue = '';
      }else if(n === '%'){
        this.calculatorValue = this.calculatorValue / 100 + '';
      }else if(
        ['/','*','+','-'].includes(n)
      ){
        this.operator = n;
        this.calculatorValue += ' ' + n + ' ';
      }else if(n==="="){
        this.calculatorValue = eval(this.calculatorValue);
        return;
      }
    }
  },
  data(){
    return {
      calculatorValue: '',
      calculatorElements:[
        'C', '*', '/', '-', 7, 8, 9, '+', 4, 5, 6, '%', 1, 2, 3, '=', 0, '.' 
      ],
      operator: '',
      evalArray: [],
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
  .bg-vue-dark{
    background:#31475e;
  }

  .hover-class:hover{
    cursor: pointer;
    background: #3d5875;
  }

  .bg-vue-green{
    background-color: #3fb984;
  }
</style>
