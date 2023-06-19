<template>
  <div class="game-container" tabindex="0" @keydown="movePlayer">
  <img src="/img/objects/trees.png" alt="">
    <Player
      class="player"
      character="polly"
      :direction="playerData.direction"
      :style="`top: ${coord.top}px; left: ${coord.left}px; `"
    />
  </div>
</template>

<script setup>
// https://www.pngegg.com/en/png-bzbpq

import { reactive } from "vue";

const coord = reactive({
  top: 0,
  left: 0,
});

const options  = reactive({
  speed: 5,
});

const playerData = reactive({
  direction: 'up',
});

function movePlayer(event) {
  if (event.code === "ArrowUp" || event.code === "KeyW") {
    playerData.direction = 'up'
    coord.top-=options.speed;
  } else if (event.code === "ArrowRight" || event.code === "KeyD") {
    playerData.direction = 'right'
    coord.left+=options.speed;
  } else if (event.code === "ArrowDown" || event.code === "KeyS") {
    playerData.direction = 'down'
    coord.top+=options.speed;
  } else if (event.code === "ArrowLeft" || event.code === "KeyA") {
    playerData.direction = 'left'
    coord.left-=options.speed;
  }
}
</script>

<style scoped>
.game-container {
  position: relative;
  width: 100%;
  height: 100vh;
  overflow: hidden;
  background-image: url('/img/textures/grass.jpg');
  background-size: 300px;
}
.game-container img {
    max-width: 100%;
    height: 1000px;
}

.player {
  position: absolute;
  left: 50%;
}
</style>

