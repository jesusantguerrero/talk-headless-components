<template>
  <button 
    class="flex" 
    @click="setCurrent(current)" 
    @mouseover="setHovered(current)"
    @mouseout="setHovered(0)">
       <slot>
          {{ current }}
        </slot>
  </button>
</template>

<script setup>
  import { inject } from "vue"

  defineProps({
    current: { type: Number }
  })

  const { setCurrent, setHovered, } = inject('controls')
</script>

<style lang="css">
.visuallyhidden {
  display: none
}
</style>