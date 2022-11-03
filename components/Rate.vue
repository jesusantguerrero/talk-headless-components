<template>
 <h4 class="mt-4 mb-1 font-bold text-blue-900">How useful is the topic?</h4>
   <BareRate v-model="rating" :count="5" class="space-x-2 cursor-pointer" v-slot:default="{ selected, covered, current, setHovered }">
     <button 
          @click="rating=current" 
          @mouseover="setHovered(current)"
          @mouseout="setHovered(0)"
          class="font-bold text-gray-400 transition transform cursor-pointer hover:text-yellow-400 hover:scale-110" 
          :class="[(selected || covered) ? 'text-yellow-500': 'text-gray-400']"
      > 
       <svg width="32" height="32" viewBox="0 0 24 24"><path fill="currentColor" d="m5.825 22l1.625-7.025L2 10.25l7.2-.625L12 3l2.8 6.625l7.2.625l-5.45 4.725L18.175 22L12 18.275Z"/></svg>
     </button>
   </BareRate>
</template>

<script setup>
  import BareRate from "./BareRate.vue"
  import { ref } from "vue"
  
  const rating = ref(0)

</script>