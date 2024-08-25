<script setup>
import { ref } from "vue";
import StopWatch from "./components/StopWatch.vue";

const items = ref(1);
</script>

<template>
  <div>
    <header>
      <a href="./">
        <h1>Stop Watch</h1>
        <div>Example by marcincook</div>
      </a>
      <button @click="items++">+</button>
    </header>

    <div class="modules">
      <StopWatch
        v-for="i in items"
        class="module"
        :name="'Timer ' + i"
        :key="i"
      />
    </div>
  </div>
</template>

<style scoped>
header {
  margin-bottom: 1rem;
  text-align: left;
  padding-inline: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
h1 {
  line-height: 1;
  margin-top: 0;
}
header button {
  font-size: 1.5rem;
}

.modules {
  border: 1px solid rgb(234, 234, 234);
  border-radius: 2rem 2rem 0 0;
  margin-inline: auto;
  padding: 1rem;
  display: grid;
  grid-template-columns: repeat(auto-fill, minmax(350px, 1fr));
  gap: 1rem;
  background-color: rgb(255, 255, 255);
  box-shadow: 0 -5px 5px rgba(0, 0, 0, 0.03);
}

.module {
  border: 1px solid rgb(213, 213, 213);
  border-radius: 1.5rem;
  /* flex-basis: clamp(min(350px, 100%), 350px, 100%); */
  /* flex-grow: 1; */
  padding: 0.5rem;
}
</style>
