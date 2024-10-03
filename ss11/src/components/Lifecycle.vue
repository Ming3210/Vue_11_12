<template>
  <div>
    <button @click="change">increase</button>
    <p>{{ cal }}</p>
    <p>{{ cal2() }}</p>
  </div>
</template>

<script setup>
import {
  computed,
  onBeforeMount,
  onBeforeUpdate,
  onMounted,
  onUpdated,
  ref,
} from "vue";

// update

onMounted(() => {
  console.log("on mounted");
});
onBeforeMount(() => {
  console.log("on before mount");
});
onBeforeUpdate(() => {
  console.log("on before update");
});
onUpdated(() => {
  console.log("on updated");
});
const a = ref(2);
const b = ref(2);

const cal = computed(() => {
  return a.value * 2;
});
const cal2 = () => {
  return b.value * 2;
};
const change = () => {
  a.value++;
};
</script>

<style></style>
