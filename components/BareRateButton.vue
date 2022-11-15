<template>
  <button 
    class="flex" 
    @click="setSelected(itemNumber)" 
    @mouseover="setHovered(itemNumber)"
    @mouseout="setHovered(0)">
       <slot>
          {{ itemNumber }}
        </slot>
  </button>
</template>

<script setup>
  import { inject } from "vue"

  defineProps({
    itemNumber: { type: Number }
  })

  const { setSelected, setHovered } = inject('controls')
</script>

<style lang="css">
.visuallyhidden {
  display: none
}
</style>