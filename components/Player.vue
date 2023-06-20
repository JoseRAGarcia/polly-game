<template>
  <div class="player-container">
    <img
      :src="`/img/characters/${character}/moving-${direction}-${position}.png`"
      alt=""
    />
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const props = defineProps({
  character: {
    type: String,
    default: "polly",
  },
  direction: {
    type: String,
    default: "up",
  },
  moving: {
    type: Boolean,
    default: false,
  },
});

const position = ref(2);
let timer = ref(null);
const characterClass = ref("walker");

onMounted(() => {
  setCharacterClass();
});

onUnmounted(() => {
  stopWalking();
});

watch(
  () => props.moving,
  (newValue) => {
    if (characterClass.value === "flyer") return;

    if (newValue) {
      startWalking();
    } else {
      stopWalking();
    }
  }
);

function setCharacterClass() {
  switch (props.character) {
    case "polly":
      characterClass.value = "flyer";
      break;
    case "ramon":
      characterClass.value = "walker";
      break;
  }

  if (characterClass.value === "flyer") {
    startWalking();
  } else {
    position.value = 2;
  }
}

function startWalking() {
  timer = setInterval(() => {
    position.value < 4 ? position.value++ : (position.value = 1);
  }, 300);
}
function stopWalking() {
  position.value = 2
  clearInterval(timer);
  //timer.value = null;
}
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