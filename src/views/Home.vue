<template>
  <div class="home">
    <!-- 
    <div>
        <h1>Counter - {{counter}}</h1>
        <button @click="counter++">Click</button>
      </div>
      <div>
        <h1>counter2 - {{counter2}}</h1>
        <input @keyup="keyUpMethod"/>
      </div>
      -->
    <div id="calc">
      <div id="calc2">
        <input type="checkbox" id="checkbox" v-model="showKey">
        <label for="checkbox">Показать клавиатуру</label>

        <div id="calcDisplay">
          <!--
          <div class="display">
            fib(<input v-model.number="operand1" />)
            fib(<input v-model.number="operand2" />)
            = {{ fibResult }}
          </div>
          -->

          <input type="radio" id="one" value="operand1" name="selNum"  v-model="checkedNames">
          <label for="one">Один</label>
          <input for="one"  v-model.number="operand1" />
          <br>
          <input type="radio" id="two" value="operand2" name="selNum" v-model="checkedNames">
          <label for="two">Два</label>
          <input for="two" v-model.number="operand2" />
          <div v-if="error">{{ error }}</div>
          <div v-else> = {{result}}</div>
          <!--
          <input for="one" v-model.number="operand1" />
          <p v-if="checkedNames==111">{{ operand1 }},{{ operand1+1 }}</p>
          <p v-else>{{ checkedNames }},{{ checkedNames.value }},{{ checkedNames.id }}</p>
          
          <div v-show="error">{{ error }}</div>
          v-if вставляет или удаляет элемент а v-show скрывает или показывает
          
          
          <div class="strange-message">
            <template v-if="result < 0">Получилось отрицательное число</template>
            <template v-else-if="result < 100">Результат в первой сотне</template>
            <template v-else>Получилось слишком большое число</template>
          </div>
-->   
          
        </div>
        
        <div id="board">
          <button v-for="item in operands" :key = "item" @click="calculate(item)" v-bind:title="item">
            {{ item }}
          </button>
        <div v-if="showKey">
            <button v-for="item in numbers" :key = "item" v-bind:title="item" @click="putNumber(item)">
                {{ item }}
            </button>
        </div>
        <h2 v-else>Здесь могла бы быть ваша клавиатура</h2>
     </div>   
        
    </div>
    </div>
    <div class="logs">
     <div v-for="(log, id) in logs" v-bind:key="id">{{ log }}</div>
   </div>
    <img alt="Vue logo" src="../assets/logo.png">
    <HelloWorld msg="Welcome to Your Vue.js App"/>
    
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'
import Vue from 'vue'

export default {
  name: 'Home',
  components: {
    HelloWorld
  },
  data(){
       return {
         //counter:0,
         //counter2:0,
           operand1: 0,
           operand2: 0,
           result:0,
           error: '',
           numbers: ["1","2","3","4","5","6","7","8","9","0",",","Delete"],
           operands: ["+","-","*","/","pow","%"],
           logs: {},
           fibResult:0,
           showKey:false,
           checked:false,
           checkedNames: false,
       }
      },/*
      computed: {
        fibb1 () {
          return this.fib(this.operand1)
        },
        fibb2 () {
          return this.fib(this.operand2)
        },
      },*/

   
    methods:{
      /*
      keyUpMethod(){
        this.counter2++
      },
      
     fib(n) {
     return n <= 1 ? n : this.fib(n - 1) + this.fib(n - 2);
   },*/

     calculate (operation = '+') {
       this.error = ''
     switch (operation) {
       case '+':
         this.plus()
         break;
       case '-':
         this.minus()
         break;
       case '*':
         this.multy()
         break;
       case '/':
         this.div()
         break;
      case 'pow':
         this.pow()
         break;
      case '%':
         this.ostDiv()
         break;
     }
     const key = Date.now()
  const value = `${this.operand1}${operation}${this.operand2}=${this.result}`
  Vue.set(this.logs, key, value)

     
   },
   putNumber(item){
      switch (this.checkedNames) {
        case 'operand1':
          if (item == "Delete"){
            let delNumber=String(this.operand1);
            this.operand1=Number(delNumber.substring(0, delNumber.length - 1));
            }
          else 
            this.operand1=Number(String(this.operand1) + item)
          break;
          case 'operand2':
          if (item == "Delete"){
            let delNumber=String(this.operand2);
            return this.operand2=Number(delNumber.substring(0, delNumber.length - 1));
            }
          else
            this.operand2=Number(String(this.operand2) + item)
          break;
      }
        
      },
       /*
       else if (item==","){
         if (this.checkedNames){
         //alert(typeof(this.checkedNames))
         alert( this.checkedNames )}

       }*/

      
      plus(){
         this.result = this.operand1 + this.operand2
         this.fibResult = this.fibb1 + this.fibb2

      },
      multy(){
         this.result = this.operand1 * this.operand2
         this.fibResult = this.fibb1 * this.fibb2

      },
      minus(){
         this.result = this.operand1 - this.operand2
         this.fibResult = this.fibb1 - this.fibb2

      },
      div(){
        const { operand1, operand2 } = this
        if (operand2 === 0) {
          this.error = 'Делить на 0 нельзя!'
        } else {
          this.result = operand1 / operand2
          this.fibResult = this.fibb1 / this.fibb2
        }
      },
      pow(){
        this.result= Math.pow(this.operand1 , this.operand2)
        this.fibResult = Math.pow(this.fib1 , this.fib2) 
 
      },
      ostDiv(){
        this.result=this.operand1 % this.operand2
        this.fibResult = this.fibb1 % this.fibb2

      },
   },

  
}
</script>

<style scoped>

#calc{
  width: 230px;
  height: 320px;
  outline: 1px solid grey;
  border-radius: 10px;
  box-sizing: border-box;
  padding: 29px 7px 7px;
  background-color: rgb(215, 241, 255);
  
}
#calc2{
  box-sizing: border-box;
  outline: 1px solid grey;
  width: 216px;
  height: 284px;
  padding: 10px 13px 13px;
  align-items: center;
  background-color: rgb(221, 231, 243);
}
#calcDisplay{
  outline: 1px solid grey;
  max-width: 190px;
  max-height: 320px;
  border-radius: 3px;
  background-color: rgb(244, 248, 250);
  /*display: flex;
  justify-content: space-between;*/
}
#board{
  /*outline: 1px solid grey;*/
  border-radius: 5px;
  height: 170px;
  
}
input{
  max-width: 100px;
  font-size: 16px;
  background-color:  rgb(244, 248, 250);
  /*border: none;*/
} 
button{
  height: 30px;
  min-width: 33px;
  font-size: 16px;
  margin-left: 5px;
  margin-top: 5px;
  background-color: rgb(213, 224, 238);
  border-radius: 5px;
  border: 1px solid grey;

} 
</style>

