<script setup lang="ts">

/* Just a simple screen that displays a string (easier for my aplication tho isnt good for the future when i try to make complex calculation)*/
const props = defineProps({
  valor: { type: String, default: "0" }
})
</script>

<template>
    <div class="container">
        <div class="conteudo">
            <p class="telaNum">{{ valor }}</p>
        </div>
    </div>


</template>

<style scoped>
@import url('https://fonts.googleapis.com/css2?family=Press+Start+2P&family=Quantico:ital,wght@0,400;0,700;1,400;1,700&display=swap');

.container{
    font-family: "Press Start 2P"
}


</style>
