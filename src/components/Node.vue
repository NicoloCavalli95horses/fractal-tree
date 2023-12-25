<template>
  <div class="canvas" :style="{ 'width': `${size}px`, 'height': `${size}px`, 'transform' : `translate(-50%, -50%) scale(${scale})`}">
    <svg width="100%" height="100%">
      <line x1="0" y1="0" x2="50%" y2="50%" stroke="#eee" />
      <line :x1="size" y1="0" x2="50%" y2="50%" stroke="#eee" />
      <circle :cx="size/2" :cy="size/2" r="10" fill="#eee" />
    </svg>
    <div v-if="level < max_levels" class="child left">
      <Node :x1="0" :size="size-100" :max_levels="max_levels" :level="level + 1" :scale="scale" />
    </div>
    <div v-if="level < max_levels" class="child right">
      <Node :x1="100" :size="size-100" :max_levels="max_levels" :level="level + 1" :scale="scale" />
    </div>
  </div>
</template>

<script setup>
//======================
// Import
//======================
import {
  onMounted,
} from "vue";

import Node from './Node.vue';

//======================
// Const
//======================
const props = defineProps({
  x1: Number,
  level: {
    type: Number,
    default: 1,
  },
  scale: {
    type: Number,
    default: 1
  },
  max_levels: {
    type: Number,
    default: 3,
  },
  size: {
   type: Number,
   default: 100,
  }
});

const emit = defineEmits([
  'mounted',
]);

//======================
// Life cycle
//======================
onMounted(() => {
  emit("mounted");
});

</script>


<style scoped lang="scss">
.canvas {
  position: absolute;
  top: 95%;
  left: 50%;
  .child {
    position: absolute;
    top: 0;
    transform: translate(-50%, -50%);
    &.left {
      left: 0;
    }
    &.right {
      right: 0;
    }
  }
}
</style>