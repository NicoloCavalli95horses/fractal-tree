<template>
  <div class="main">
    <Node :style="{ 'transform' : `scale(${scale})` }" :max_levels="7" :size_px="700" />
  </div>
</template>

<script setup>
//======================
// Import
//======================
import {
  ref,
  onMounted,
  onUnmounted
} from 'vue';

import Node from './components/Node.vue';


const INCREMENT = 0.05;
const scale = ref( -0.65 );

//======================
// Function
//======================
function onWheel(e) {
  const zoom_in = e.deltaY < 0;
  scale.value = zoom_in ? scale.value + INCREMENT : scale.value - INCREMENT; 
  console.log(scale.value)
}


//======================
// Life cycle
//======================
onMounted(() => {
  window.addEventListener("wheel", onWheel);
});

onUnmounted(() => {
  window.removeEventListener("wheel", onWheel);
});
</script>

<style lang="scss" scoped>
.main {
  width: 100vw;
  height: 100vh;
}

</style>
