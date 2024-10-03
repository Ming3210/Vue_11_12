<template>
  <div>asdasd</div>
</template>

<script setup>
import { onBeforeUnmount, onUnmounted } from "vue";

onBeforeUnmount(() => {
  console.log("Component is about to be unmounted");
});

onUnmounted(() => {
  console.log("Component has been unmounted");
});
</script>

<style></style>
