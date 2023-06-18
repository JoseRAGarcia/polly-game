<template>
    <div class="player-container">
        <img :src="`assets/img/characters/polly/moving-${direction}-${position}.png`" alt="">
    </div>
</template>

<script setup>
import {ref, onMounted, onUnmounted} from 'vue'

const props = defineProps({
    direction: {
        type: String,
        default: 'up'
    },
})

onMounted(() => {
  timer = setInterval(() => {
    position.value < 3 ? position.value++ : position.value = 1
  }, 300);
})

onUnmounted(() => {
  clearInterval(timer)
  timer.value = null
})

const position = ref(1)
let timer = ref(null)
</script>

<style scoped>
.player-container {
    width: 100px;
    height: 100px;
    overflow: hidden;
    display: flex;
    align-items: center;
    justify-content: center;
}

.player-container img {
    max-width: 100%;
    max-height: 100%;
}
</style>