<template>
  <label 
    class="flex" 
    @click="setCurrent(current)" 
    @mouseover="setHovered(current)"
    @mouseout="setHovered(0)">
    <input 
      :value="current" 
      :id="`rate${current}`"
		  type="radio" 
      name="rating" 
      class="visuallyhidden"
      @click="setCurrent(current)" 
      @mouseover="setHovered(current)"
      @mouseout="setHovered(0)"
     >
      <span class="visuallyhidden">{{current}} Star</span>
       <slot />
  </label>
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