<template>
  <div class="flex" @submit.prevent>
    <slot
        v-for="index in state.range" 
        :key="index" 
        :itemNumber="index+1"
        :selected="isSelected(index+1)"
        :covered="isCovered(index+1)"
        :setHovered="setHovered"
    />
  </div>
</template>

<script setup>
import { computed, reactive, provide, toRefs } from "vue";

const props = defineProps({
  modelValue: { type: Number },
  count: { type: Number }
});

const emit = defineEmits(['update:modelValue']);

const state = reactive({
  lastHoveredItem: 0,
  range: computed(() => {
    return [...Array(props.count).keys()];
  }),
})

// state functions
function isCovered(index) {
  return index <= state.lastHoveredItem || index <= props.modelValue;
}

function isSelected(index) {
  return props.modelValue == index;
}

function setHovered(index) {
  state.lastHoveredItem = index;
}

const setSelected = (index) => {
  emit('update:modelValue', index)
}

provide('controls', {
  isSelected,
  setHovered,
  setSelected
})
</script>