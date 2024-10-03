<template>
  <div>
    <h1>B4</h1>
    <button @click="click">Increase Age</button>
    <p>Age : {{ age }}</p>
    <Exercise04Children :props="age" />
  </div>
</template>

<script setup>
import { ref } from "vue";
import Exercise04Children from "./Exercise04Children.vue";

const age = ref(1);
const click = () => {
  age.value++;
};
</script>

<style></style>
