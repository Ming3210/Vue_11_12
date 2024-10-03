<template></template>

<script setup>
import { onUpdated } from "vue";

const props = defineProps(["props"]);

onUpdated(() => {
  console.log("Updated");
});
</script>

<style></style>
