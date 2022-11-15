<template>
 <h4 class="mt-4 mb-1 font-bold text-white">How useful is the topic?</h4>
   <BareRate v-model="rating" :count="5" class="space-x-2 cursor-pointer" v-slot:default="{ selected, covered, itemNumber, setHovered }">
     <button 
          @click="rating=itemNumber" 
          @mouseover="setHovered(itemNumber)"
          @mouseout="setHovered(0)"
          class="font-bold transition transform cursor-pointer  hover:scale-110" 
          :class="[selected || covered ? 'text-yellow-400': 'text-gray-400']"
      > 
       <mdi-star />
     </button>
   </BareRate>

   {{ selected }}
</template>

<script setup>
  import { ref } from "vue"
  
  const rating = ref(0)

</script>