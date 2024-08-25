<script setup>
import StopWatch from "./components/StopWatch.vue";
</script>

<template>
  <div class="modules">
    <StopWatch v-for="i in 9" class="module" :name="'Timer ' + i" :key="i" />
  </div>
</template>

<style scoped>
.modules {
  border: 1px solid rgb(236, 236, 236);
  border-radius: 2rem;
  max-width: 100%;
  margin-inline: auto;
  padding: 1rem;
  display: grid;
  /* grid-auto-columns: clamp(300px, 350px, 100%); */
  grid-template-columns: repeat(3, 1fr);
  gap: 1rem;
  background-color: rgb(255, 255, 255);
  box-shadow: 1px 5px 10px rgba(0, 0, 0, 0.1);

  margin: 0 auto;
}
.module {
  border: 1px solid rgb(193, 193, 193);
  border-radius: 1.5rem;
  /* width: clamp(min(10vw, 20rem), 400px, max(90vw, 55rem)); */
  padding: 1rem;
}
.module-1 {
  background-color: lightblue;
}
.module-2 {
  background-color: lightskyblue;
}
</style>
