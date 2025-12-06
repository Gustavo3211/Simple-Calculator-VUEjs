<script setup lang="ts">
/* Receives the value from the parent component. Defaults to "0" */
const props = defineProps({
  valor: { type: String, default: "0" }
})
</script>

<template>
    <div class="container">
        <div class="conteudo scan-text" style="display: flex; align-items: flex;">
            
            <p class="telaNum" :class="{ 'blink': valor === '' }">
                {{ valor === '' ? '>' : valor }}
            </p>

            <p v-show="valor != ''" class="blink">
                <
            </p>
        </div>
    </div>
</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Quantico:ital,wght@0,400;0,700;1,400;1,700&display=swap');

.container{
    font-family: "Press Start 2P";   
}

/* --- SCANLINE ANIMATION --- */

/* Creates the top-to-bottom movement */
@keyframes scanline-scroll {
  0% { background-position: 0% 0%; }     
  100% { background-position: 0% 200%; } 
}

.scan-text {   

    background: linear-gradient(
        250deg,
        rgba(59, 66, 58, 1) 0%, 
        rgb(74, 80, 59) 50%, 
        rgba(59, 66, 58, 1) 100%
    );


    background-size: 100% 200%;


    -webkit-background-clip: text;
    background-clip: text;
    
    color: transparent;
    animation: scanline-scroll 0.2s linear infinite;
}

/* --- BLINK ANIMATION --- */

@keyframes blink-effect {
  0% { opacity: 1; }
  50% { opacity: 0; }
  100% { opacity: 1; }
}

.blink{
  animation: blink-effect 1s infinite; 

  animation-timing-function: step-start;
}
</style>