<script setup lang="ts">
import Tela from './components/Screen.vue';
import { ref, onMounted } from 'vue'

onMounted(() => {
  num.value = 'Hi! :)'
});

/* VAR DEFINITION */
const num = ref('');
const operation = ref('');



/* HANDLE THE DIGIT OPERATION */
const addDigit = (event: MouseEvent) => {
  const target = event.target as HTMLButtonElement;
  const digit = target.value;

  /*handle the override after showing results */
  if (showingResult.value === true){
    num.value = num.value + digit;
    showingResult.value = false

  } else {

    /* handle the override for the first digit */
    if (num.value === '' || num.value === 'Hi! :)'){
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
  operation.value = ""
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
<div class="Table">

<div class="Calculator">
  <div class="Container">
      <div class="Screen">
        <tela :valor="num"></tela>
        <span v-if="num.length <= 15"style="color: transparent;justify-content: end !important;" class="material-symbols-outlined">stat_minus_1</span>
        
        <span v-if="num.length >= 15"style="color: #3b423a;justify-content: end !important;" class="material-symbols-outlined">stat_minus_2</span>
      </div>

      <div class="Button-top">
          <a target="_blank" href="https://github.com/Gustavo3211/Simple-Calculator-VUEjs"><button class="button-fn"><span class="material-symbols-outlined">hub</span>git</button></a>
          <a target="_blank" href="https://polyhaven.com/a/plank_flooring_04"><button><span class="material-symbols-outlined">texture</span>bg</button></a>
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
                    <button @click="addDigit($event)" value="00">00</button>
                    <button @click="addDigit($event)" value=",">,</button>
                
            </div>
            <div class="botao-side-l">
                    <button @click="num='';operation=''">AC</button>
                    <button @click="handleoperator($event)" value="+">+</button>
                    <button @click="handleoperator($event)" value="-">-</button>
                    <button @click="handleoperator($event)" value="/">/</button>
                    <button @click="handleoperator($event)" value="x">x</button>
                  <button @click="display(num)">=</button>
          </div>
      </div>
  </div>
</div>

</div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Quantico:ital,wght@0,400;0,700;1,400;1,700&display=swap');


.Table{
  display: flex;
  justify-content: center;
  align-items: center;
  width: 100vw;
  height: 100vh;
  background-image: url(https://dl.polyhaven.org/file/ph-assets/Textures/jpg/1k/plank_flooring_04/plank_flooring_04_diff_1k.jpg);
  background-repeat: repeat;
}

.Calculator {
  font-size: 2vmin;
  width: 20em;
  max-width: 20em;
  height: 45em;
  max-height: 45em;
  border: 0.3em solid #a1c405;
  background-color: rgb(231, 231, 231);
  box-shadow: 0.5em 0.5em 1em rgb(0, 0, 0);
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 1em;
  border-radius: 1em;
}
.Button-top {
  margin-bottom: 0.3em;
  display: flex;
  gap: 0.5em;
  flex-shrink: 0;
  grid-template-columns: repeat(3, 4em);
}
.Button-top span{
  font-size: 1.5em;
}
.Container {
  display: flex;
  flex-direction: column;
  width: 18em;
}

.botoes {
  display: flex;
}

.Screen {
  width: 100%;
  margin-bottom: 1em;
  word-break: break-all;
  background-color: #6d7659;
  height: 4em;
  min-height: 4em;
  max-height: 4em;
  overflow-y: auto;
  padding: 0.5em;
  font-size: 1.5em;
  display: flex;
  justify-content: flex-start;
  border: 3px solid rgba(231, 231, 231, 0.685);
  border-radius: 0.5em;
}




.ButtonsWrapper {
  display: flex;
  gap: 0.5em;
  align-items: flex-start;
}

.botao-num {
  display: grid;
  grid-template-columns: repeat(3, 4em);
  gap: 0.5em;
  flex-shrink: 0;

}

.botao-side-l {

  display: flex;
  flex-direction: column;
  gap: 0.5em;
  flex-shrink: 0;
}

button {
  font-family: "Quantico";
  width: 4em;
  height: 4em;
  font-size: 1em;
  cursor: pointer;
  border-radius: 2em;
  border: none;
}

button:active {
  filter: brightness(1.3); /* Efeito de clique */
}

.botao-num button {
  background-color: var(--btn-num-bg);
  color: var(--btn-num-text);
}

.botao-side-l button {
  background-color: var(--btn-op-bg);
  color: var(--btn-op-text);
}

.botao-side-l button:first-child {
  background-color: var(--btn-ac-bg);
  color: var(--btn-ac-text);
}

.button-fn{
  background-color: #104C35 !important;
}


</style>