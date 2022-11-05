<template>
    <h4 class="mt-4 mb-1 font-bold text-white">How useful is the topic?</h4>
    <article class="flex justify-between">
       <BareRate v-model="rating" :count="5" class="space-x-2 cursor-pointer" v-slot:default="{ selected, covered, current }">
         <BareRateButton 
             :current="current"
             class="px-3 py-0.5 font-bold border border-gray-400 transition transform rounded-lg cursor-pointer hover:text-blue-400" 
             :class="{'text-blue-500 border-blue-500 shadow-md ring ring-blue-200': selected}"
         />
       </BareRate>
    </article>
  </template>
  
  <script setup>
    import { ref } from "vue"
  
    const rating = ref(0)
  </script>