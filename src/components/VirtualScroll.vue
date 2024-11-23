<template>
  <div ref="containerRef" class="container" @scroll="handleScroll">
    <div class="phantom" :style="{ height: phantomHeight + 'px' }"></div>
    <div class="list" :style="{ transform: `translateY(${offset}px)` }">
      <div
        class="item"
        :style="{ height: itemHeight + 'px', lineHeight: itemHeight + 'px' }"
        v-for="item in VirtualData"
      >
        <slot name="item" :data="item"></slot>
      </div>
    </div>
  </div>
</template>
<script setup lang="ts">
import { computed, onMounted, ref } from "vue";
const screenHeight = ref<number>(0);
const phantomHeight = ref<number>(0);
const containerRef = ref<HTMLDivElement | null>(null);
const startIndex = ref<number>(0);
const endIndex = ref<number>(0);
const offset = ref<number>(0);
const props = defineProps({
  list: {
    type: Array<{ id: number; value: string }>,
    default: () => [],
  },
  itemHeight: {
    type: Number,
    default: 50,
  },
});
const VirtualData = computed(() =>
  props.list.slice(startIndex.value, endIndex.value + 1)
);
const handleScroll = () => {
  const scrollTop = containerRef.value?.scrollTop || 0;
  startIndex.value = Math.floor(scrollTop / props.itemHeight);
  endIndex.value = Math.min(
    startIndex.value + screenHeight.value / props.itemHeight,
    props.list.length
  );
  console.log(startIndex.value, endIndex.value);
  offset.value = scrollTop - (scrollTop % props.itemHeight);
};
onMounted(() => {
  screenHeight.value = containerRef.value?.clientHeight || 0;
  console.log(screenHeight.value, "1");
  phantomHeight.value = props.list.length * props.itemHeight;
  startIndex.value = 0;
  endIndex.value = Math.ceil(screenHeight.value / props.itemHeight);
});
</script>
<style scoped>
.container {
  border: 1px solid #000;
  height: 500px;
  width: 300px;
  overflow: auto;
  position: relative;
}
.phantom {
  width: 100%;
}
.list {
  width: 100%;
  position: absolute;
  left: 0;
  top: 0;
}
</style>
