<script setup>
import { onMounted, ref } from "vue";
import StopWatch from "./components/StopWatch.vue";

const items = ref([
  { id: 1, name: "Timer 1" },
  { id: 2, name: "Timer 2" },
  { id: 3, name: "Timer 3" },
  { id: 4, name: "Timer 4" },
]);

const socketHost = import.meta.env.VITE_REVERB_HOST;
onMounted(() => {
  console.log("VITE_REVERB_HOST", socketHost);
});

// Echo.join("test")
//   .here((users) => {
//     usersHere = users;
//   })
//   .joining((user) => {
//     usersHere.push(user);
//   })
//   .leaving((user) => {
//     usersHere = usersHere.filter((u) => u.id !== user.id);
//   });

Echo.channel("test")
  .listen("TestEvent", (event) => {
    console.log(event);
    items.value.map((item) => {
      if (item.id === event.message.id) {
        item.name = event.message.body;
      }
    });
  })
  .listen("NewTimer", (event) => {
    console.log(event);
    items.value.push(event);
  });

function addTimer() {
  const id = items.value.length + 1;
  items.value.push({ id: id, name: "Timer " + id });
}
</script>

<template>
  <div>
    <header>
      <a href="./">
        <h1>Stop Watch</h1>
        <div>Example by marcincook</div>
      </a>
      <button @click="addTimer">+</button>
    </header>

    <div class="modules">
      <StopWatch
        v-for="item in items"
        class="module"
        :name="item.name"
        :key="item.id"
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
  grid-template-columns: repeat(auto-fill, minmax(400px, 1fr));
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
