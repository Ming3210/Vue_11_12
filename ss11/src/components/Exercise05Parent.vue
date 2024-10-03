<template>
  <div>
    <h1>B5</h1>
    <button @click="click">Toggle</button>
    <Exercise05Children v-if="isShow" />
  </div>
</template>

<script setup>
import { onBeforeUnmount, onUnmounted, ref } from "vue";
import Exercise05Children from "./Exercise05Children.vue";

onBeforeUnmount(() => {
  console.log("Component is about to be unmounted");
});

const isShow = ref(true);
const click = () => {
  isShow.value = !isShow.value;
};

onUnmounted(() => {
  console.log("Component has been unmounted");
});
</script>

<style></style>
