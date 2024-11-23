<template>
  <h2>guang的虚拟列表</h2>
  <VirtualScroll :list="listData">
    <template #item="{ data }">
      <div class="item">
        <span>序号：{{ data.id }}</span>
        <span>内容：{{ data.value }}</span>
      </div>
    </template>
  </VirtualScroll>
</template>
<script setup lang="ts">
import VirtualScroll from "./components/VirtualScroll.vue";
import { ref } from "vue";
const listData = ref(
  new Array(1000000)
    .fill(null)
    .map((_, i) => ({ id: i, value: `第${i}个Item` }))
);
</script>
<style scoped>
h2 {
  text-align: center;
  margin-bottom: 20px;
  border: 1px solid #56ab3a;
  border-radius: 5px;
}
.item {
  display: flex;
  justify-content: space-around;
  align-items: center;
  text-align: center;
  border: 1px solid #e261d3;
  margin: 5px;
  background-color: #f2fa0c;
}
</style>
