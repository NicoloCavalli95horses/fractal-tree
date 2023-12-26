<template>
  <div class="main">
    <div class="canvas" :style="{ 'width': `${size_px}px`, 'height': `${size_px}px`}">
      <svg width="100%" height="100%">
        <line x1="0" y1="0" x2="50%" y2="50%" :stroke="rand_color" stroke-width="2%" />
        <line x1="50%" y1="0" x2="50%" y2="50%" :stroke="rand_color" stroke-width="2%" />
        <line x1="100%" y1="0" x2="50%" y2="50%" :stroke="rand_color" stroke-width="2%" />
        <circle cx="50%" cy="50%" r="4%" :fill="rand_color" />
      </svg>
      <template v-if="level < max_levels">
        <Node class="child left" :size_px="size_px/PHI" :max_levels="max_levels" :level="level+1" />
        <Node class="child center" :size_px="size_px/PHI" :max_levels="max_levels" :level="level+1" />
        <Node class="child right" :size_px="size_px/PHI" :max_levels="max_levels" :level="level+1" />
      </template>
    </div>
  </div>
</template>

<script setup>
//======================
// Import
//======================
import Node from './Node.vue';


//======================
// Const
//======================
const props = defineProps({
  level: {
    type: Number,
    default: 1,
  },
  max_levels: {
    type: Number,
    default: 3,
  },
  size_px: {
   type: Number,
   default: 100,
  }
});

const PHI = 1.618033988749895;
const rand_color = `hsla(${Math.random() * 360}, 100%, 50%, 1)`;

</script>


<style scoped lang="scss">
.canvas {
  position: absolute;
  transform: translate(-50%, -50%);
  top: 110%;
  left: 50%;
}
.child {
  position: absolute;
  top: 0;
  transform: translate(-50%, -50%);
  &.left {
    left: 0;
  }
  &.center {
    left: 50%;
  }
  &.right {
    right: 0;
  }
}

</style>