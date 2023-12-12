<script setup>
import HelloWorld from "./components/HelloWorld.vue";
import TheWelcome from "./components/TheWelcome.vue";
</script>

<template>
  <h1>실습</h1>
  <input id="input" type="text" v-bind:placeholder="message" />
</template>

<script>
const app = Vue.createApp({
  data() {
    return {
      message: "값을 입력해주세요!",
    };
  },
});
app.mount("#input");
</script>

<style scoped></style>
