<template>
  <div>
    <slot
        v-for="current in state.range" 
        :key="current" 
        :current="current+1"
        :selected="isSelected(current+1)"
        :covered="isCovered(current+1)"
        :setHovered="setHovered"
    >
        {{ current }}
    </slot>
  </div>
</template>

<script setup>
import { ref, computed, reactive, provide } from "vue";

const props = defineProps({
  modelValue: { type: Number },
  count: { type: Number }
});

const emit = defineEmits(['update:modelValue']);

const state = reactive({
  hoveredIndex: 0,
  range: computed(() => {
    return [...Array(props.count).keys()];
  }),
})

// state functions
function isCovered(index) {
  return index <= state.hoveredIndex
  || index <= props.modelValue;
}

function isSelected(index) {
  return props.modelValue == index;
}

function setHovered(index) {
  state.hoveredIndex = index;
}

const setCurrent = (index) => {
  emit('update:modelValue', index)
}

provide('controls', {
  setCovered,
  isSelected,
  setHovered,
  setCurrent
})

const { modelValue } = toRefs(props)
provide('value', modelValue);

</script>