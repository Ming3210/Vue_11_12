<template>
  <div>
    <h1>B8</h1>
    <p>Chiều rộng cửa sổ hiện tại: {{ width }}px</p>
  </div>
</template>

<script setup>
import { ref, onMounted, onUnmounted } from "vue";

const width = ref(window.innerWidth);

const updateWidth = () => {
  width.value = window.innerWidth;
};

onMounted(() => {
  window.addEventListener("resize", updateWidth);
});
</script>

<style scoped>
div {
  background-color: #f0f0f0;
}
</style>
