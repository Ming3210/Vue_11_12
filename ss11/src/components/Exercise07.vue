<template>
  <div>
    <h1>B7</h1>
    <input v-model="input" type="text" />
  </div>
</template>

<script setup>
import { onBeforeMount, onMounted, ref, watch } from "vue";

const input = ref("");
const updateTitle = (newTitle) => {
  document.title = newTitle;
};

watch(input, (newVal) => {
  updateTitle(newVal);
});

onMounted(() => {
  updateTitle(input.value);
});
</script>

<style></style>
