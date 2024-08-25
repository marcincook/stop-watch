<script setup>
import { ref } from "vue";
const timeElapsed = ref(0);
const state = ref("stopped"); // stopped, running, paused
const interval = ref(0);

defineProps({
  name: {
    type: String,
    default: "",
  },
});

function start() {
  state.value = "running";
  interval.value = setInterval(() => {
    timeElapsed.value++;
  }, 1000);
}

function pause() {
  state.value = "paused";
  clearInterval(interval.value);
  interval.value = undefined;
}

function restart() {
  timeElapsed.value = 0;
  state.value = "running";
  if (interval.value !== undefined) {
    clearInterval(interval.value);
    interval.value = undefined;
  }
  start();
}

function reset() {
  timeElapsed.value = 0;
  state.value = "stopped";
  if (interval.value !== undefined) {
    clearInterval(interval.value);
    interval.value = undefined;
  }
}

function formatTime(elapsedTime) {
  const minutes = `0${Math.floor(elapsedTime / 60)}`.slice(-2);
  const seconds = `0${elapsedTime % 60}`.slice(-2);
  return `${minutes}:${seconds}`;
}
</script>

<template>
  <div>
    <div class="name">
      {{ name }}
    </div>
    <div class="timeElapsed">{{ formatTime(timeElapsed) }}</div>
    <div class="controls">
      <button v-if="state === 'stopped'" @click="start">start</button>
      <button v-if="state === 'running'" @click="pause">pause</button>
      <button v-if="state === 'paused'" @click="start">resume</button>
      <button v-if="state === 'running' || state === 'paused'" @click="restart">
        restart
      </button>
      <button v-if="state !== 'stopped'" @click="reset">reset</button>
    </div>
  </div>
</template>

<style scoped>
.name {
  font-weight: 500;
  font-size: 2rem;
}
.timeElapsed {
  text-align: center;
  color: rgb(104, 104, 104);
  font-size: 4rem;
  font-weight: 100;
}
.controls {
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 0.5rem;
  margin-top: 1rem;
}
</style>
