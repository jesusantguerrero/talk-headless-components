<template>
 <button 
    @click="controls.setCurrent(current)" 
    @mouseover="controls.setHovered(current)"
    @mouseout="controls.setHovered(0)"
  >
    <slot />
  </button>
</template>

<script setup>
  import { inject } from "vue"

  defineProps({
    current: { type: Number }
  })

  const controls = inject('controls')
  const value = inject('value')
</script>