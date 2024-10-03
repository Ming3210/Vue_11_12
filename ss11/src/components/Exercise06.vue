<template>
  <div>
    <h1>B6</h1>
    <button @click="increment">Counter</button>
    <p>{{ num }}</p>
  </div>
</template>

<script setup>
import { onMounted, onUpdated, ref, watch } from "vue";

const num = ref(0);

const increment = () => {
  num.value++;
};
watch(num, (newCount) => {
  document.title = `${newCount}`;
});
</script>

<style></style>
