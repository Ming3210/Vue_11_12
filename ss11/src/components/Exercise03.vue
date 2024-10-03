<template>
  <div>
    <h1>B3</h1>
    <b v-if="age < 4">Current company: {{ company[0] }}</b>
    <b v-else-if="age < 7">Current company: {{ company[1] }}</b>
    <b v-else-if="age < 11">Current company: {{ company[2] }}</b>
    <p>Age:{{ age }}</p>
    <button @click="random">Random</button>
  </div>
</template>

<script setup>
import { ref } from "vue";
const age = ref(1);
const company = ref(["Rikkei Academy", "Rikkei Education", "Rikkei Fukuoka"]);
const random = () => {
  age.value = Math.ceil(Math.random() * 10);
};
</script>

<style></style>
