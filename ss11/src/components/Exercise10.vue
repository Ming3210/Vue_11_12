<template>
  <div>
    <h1>B10</h1>
    <p>{{ clock }}</p>
  </div>
</template>

<script setup>
import { onMounted, onUnmounted, ref } from "vue";

// Khởi tạo reactive variable cho clock
const clock = ref("");

// Khai báo biến để lưu ID của setInterval
let intervalId = null;

// Hàm cập nhật thời gian
const updateTime = () => {
  const hours = new Date().getHours();
  const minute = new Date().getMinutes();
  const second = new Date().getSeconds();
  clock.value = `${hours} : ${minute} : ${second}`;
};

onMounted(() => {
  // Cập nhật thời gian ngay lập tức khi component được mount
  updateTime();
  // Thiết lập bộ đếm để cập nhật thời gian mỗi giây
  intervalId = setInterval(updateTime, 1000);
});

onUnmounted(() => {
  // Dọn dẹp bộ đếm khi component bị unmount
  if (intervalId) {
    clearInterval(intervalId);
  }
});

// Debug: Hiển thị giá trị clock trong console
console.log(clock.value, 999999);
</script>

<style scoped>
/* Bạn có thể thêm style tại đây nếu cần */
</style>
