<script setup>
import { reactive } from 'vue'
import selectedwheel from '../ui/selectwheel.vue'
const selectButton = reactive({ isGrabbing: false })
const classOut = () => {
  setTimeout(() => {
    selectButton.isGrabbing = false
  }, 64)
}
const dragStart = () => {
  selectButton.isGrabbing = true
}
const clickStart = () => {
  selectButton.isGrabbing = !selectButton.isGrabbing
}

const week = ['Mon', 'Tue', 'Wed', 'Thur', 'Fri', 'Sat', 'Sun']
</script>
<template>
  <div class="select_button_background">
    <div
      class="select_button_foreground"
      draggable="true"
      @dragstart="dragStart"
      @dragend="classOut"
      @click="clickStart"
    />
    <selectedwheel
      :is-grabbing="selectButton.isGrabbing"
      @class-out="classOut"
    />
  </div>
</template>
<style scoped>
.select_button_background {
  z-index: 5;
  position: absolute;
  left: calc(50% - 1.5rem);
  width: 3rem;
  height: 3rem;
  margin: 0 auto;
  border-radius: 50%;
  background-color: var(--color-white);
}
.select_button_foreground {
  z-index: 6;
  box-sizing: border-box;
  background: conic-gradient(
    var(--color-main-bri),
    var(--color-highlight),
    var(--color-main-bri),
    var(--color-highlight),
    var(--color-main-bri)
  );
  width: 2.2rem;
  height: 2.2rem;
  position: absolute;
  top: 0.4rem;
  left: 0.4rem;
  border-radius: 50%;
  cursor: grab;
}

.select_button_foreground:focus {
  cursor: grabbing;
}

@media (max-width: 46rem) {
  .select_button_background {
    margin: 0;
    top: 0.2rem;
  }
}
</style>
