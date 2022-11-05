<template>
  <h4 class="mt-4 mb-1 font-bold text-white">How useful is the topic?</h4>
  <article class="flex justify-between">
     <BareRate v-model="rating" :count="5" class="space-x-2 cursor-pointer" v-slot:default="{ selected, covered, current }">
       <BareRateButton 
           :current="current"
           class="font-bold transition transform cursor-pointer hover:scale-110" 
           :class="[(selected || covered) ? 'text-yellow-500': 'text-gray-400']"
       > 
        <mdi-star />
       </BareRatebutton>
     </BareRate>
  </article>
</template>

<script setup>
  import { ref } from "vue"
  
  defineProps({
    showControls: {
      type: Boolean,
      default: false
    }
  })

  const rating = ref(0)
</script>