<template>
  <div>
    <h1>B9</h1>
    <b>Ứng dụng đếm số</b>
    <p>Count :{{ sec }}</p>
  </div>
</template>

<script setup>
import { onBeforeMount, onMounted, ref, watch } from "vue";

const sec = ref(0);

onBeforeMount(() => {
  setInterval(() => {
    sec.value++;
  }, 1000);
});
</script>

<style></style>
