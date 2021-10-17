<template>
  <div class="home">
    <div>
      <div>
        <h1>Counter - {{counter}}</h1>
        <button @click="counter++">Click</button>
      </div>
      <div>
        <h1>counter2 - {{counter2}}</h1>
        <input @keyup="keyUpMethod"/>
      </div>
        <input v-model.number="operand1" type="number"/>
        <button v-on:click="result = operand1 + operand2">+</button>
        <button v-on:click="minus(operand1, operand2)">-</button>
        <button @click="multy(operand1, operand2)">*</button>

        <button v-if="operand2==0" disabled>/</button>
        <button v-else @click="result = operand1 / operand2"  >/</button>

        <button @click="pow(operand1, operand2)">pow</button>

        <button v-if="operand2==0" disabled>%</button>
        <button v-else @click="ostDiv(operand1, operand2)">%</button>

        <input v-model.number="operand2" type="number"/>
        
        <p> = {{result}}</p>
    </div>
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data(){
       return {
         counter:0,
         counter2:0,
           operand1: 0,
           operand2: 0,
           result:0,
       }
   },
   methods:{
      keyUpMethod(){
        this.counter2++
      },
      multy(op1,op2){
        this.result= op1*op2

      },
      minus(op1,op2){
        this.result= op1-op2

      },
      pow(op1,op2){
        this.result= Math.pow(op1, op2)

      },
      ostDiv(op1,op2){
        this.result= op1%op2

      },
   },

  
}
</script>

<style scoped>

</style>
