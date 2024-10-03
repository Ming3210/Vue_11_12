<template>
  <div>
    <h1>B2</h1>
    <button @click="increment">Counter</button>
    <p>{{ num }}</p>
  </div>
</template>

<script setup>
import { onMounted, onUpdated, ref } from "vue";

const num = ref(1);

const increment = () => {
  num.value++;
};
onUpdated(() => {
  console.log("Dữ liệu đã thay đổi");
});
</script>

<style></style>
