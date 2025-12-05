<script setup lang="ts">
import Tela from './components/Screen.vue';
import { ref} from 'vue'


/* VAR DEFINITION */
const num = ref('0');
const operation = ref('');

/* HANDLE THE DIGIT OPERATION */
const addDigit = (event: MouseEvent) => {
  const target = event.target as HTMLButtonElement;
  const digit = target.value;

  /*handle the override after showing results */
  if (showingResult.value === true){
    num.value = digit
    showingResult.value = false

  } else {

    /* handle the override for the first digit */
    if (num.value === '0'){
      num.value = digit;
    }else{
        num.value = num.value + digit;
      }
       
    }
  }


  /*handle the display and calculation */
const display = (numero: string) => {
  var total = ref(0);
  var totalString = ref('0');

  /* calculation  */
  var num1: number | any =  0;
  var num2: number | any =  0;

  /* define the num1 and num2 by checking the operator position (fix for negative numbers) */
  let operatorIndex = operation.value === '-'? numero.lastIndexOf('-') : numero.indexOf(operation.value)

  num1 = Number(numero.slice(0,operatorIndex)) /* before operator */
  num2 = Number(numero.slice(operatorIndex + 1)) /* after operator */

  /* debug */
  console.log(num1)
  console.log(operation.value)
  console.log(num2)


  /* operations */
  if (operation.value === "+"){
    total.value = num1 + num2
  }
  if (operation.value === "-"){
    total.value = num1 - num2
  }
  if (operation.value === "x"){
    total.value = num1 * num2
  }
  if (operation.value === "/"){
    total.value = num1 / num2
  }
  /* DISPLAY RESULT */

  totalString.value = String(total.value)
  num.value = totalString.value
  showingResult.value = true;
  console.log(total.value)
}


/* handle the basic math operations */

const handleoperator = (event: MouseEvent) => {
  const target = event.target as HTMLButtonElement;
  const op = target.value;

  /* check if is the first time that user has inputted the operator */
  if (operation.value === '') {
    operation.value = op;
    addDigit(event);
    return;
  }

  /*if isnt the first time, do the calculation and add the operator at the end for better UX */
  display(num.value);
  showingResult.value = false;
  operation.value = op;
  addDigit(event);
};

const showingResult = ref(false);

</script>

<template>

<div class="Calculator">
  <div class="Container">

      <div class="Screen">
        <tela :valor="num"></tela>
      </div>

      <div class="ButtonsWrapper">

          <div class="botao-num">
                    <button @click="addDigit($event)" value="7">7</button>
                    <button @click="addDigit($event)" value="8">8</button>
                    <button @click="addDigit($event)" value="9">9</button>
                    <button @click="addDigit($event)" value="4">4</button>
                    <button @click="addDigit($event)" value="5">5</button>
                    <button @click="addDigit($event)" value="6">6</button>
                    <button @click="addDigit($event)" value="1">1</button>
                    <button @click="addDigit($event)" value="2">2</button>
                    <button @click="addDigit($event)" value="3">3</button>
                    <button @click="addDigit($event)" value="0">0</button>
            </div>
            <div class="botao-side-l">
                    <button @click="num='0';operation=''">AC</button>
                    <button @click="handleoperator($event)" value="+">+</button>
                    <button @click="handleoperator($event)" value="-">-</button>
                    <button @click="handleoperator($event)" value="/">/</button>
                    <button @click="handleoperator($event)" value="x">x</button>
                  <button @click="display(num)">=</button>
          </div>

      </div>
  </div>

</div>

</template>

<style scoped>
.Calculator {
  width: 100vw;
  height: 100vh;
  display: flex;
  justify-content: center; /* horizontal */
  align-items: center;     /* vertical */
  
}

.Container {
  
  display: flex;
  flex-direction: column;
}

.Container {
  display: flex;
  flex-direction: column;
  width: fit-content;
}
.botoes{
  display: flex;
}
.Screen {
  margin-bottom: 10px;
}


.ButtonsWrapper {
  display: flex;
  gap: 10px;
  align-items: flex-start;
}

.botao-num {
  display: grid;
  grid-template-columns: repeat(3, 40px);
  gap: 5px;
  flex-shrink: 0;  
}

.botao-side-l {
  display: flex;
  flex-direction: column;
  gap: 5px;
  flex-shrink: 0;
}

button {
  width: 40px;
  height: 40px;
}
</style>