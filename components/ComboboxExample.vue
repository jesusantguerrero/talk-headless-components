<template>
    <div class="w-full text-gray-700 shadow-gray-800 combobox">
      <Listbox v-model="selectedItem">
        <div class="relative mt-1">
          <ListboxButton
            class="relative w-full cursor-default rounded-lg bg-white py-2 pl-3 pr-10 text-left shadow-md focus:outline-none focus-visible:border-indigo-500 focus-visible:ring-2 focus-visible:ring-white focus-visible:ring-opacity-75 focus-visible:ring-offset-2 focus-visible:ring-offset-orange-300 sm:text-sm"
          >
            <span class="block truncate">{{ selectedItem.name }}</span>
            <span
              class="pointer-events-none absolute inset-y-0 right-0 flex items-center pr-2"
            >
              <ChevronUpDownIcon
                class="h-5 w-5 text-gray-400"
                aria-hidden="true"
              />
            </span>
          </ListboxButton>
  
          <transition
            leave-active-class="transition duration-100 ease-in"
            leave-from-class="opacity-100"
            leave-to-class="opacity-0"
          >
            <ListboxOptions
              class="absolute mt-1 px-0 max-h-60 w-full overflow-auto rounded-md bg-white py-1 text-base shadow-lg ring-1 ring-black ring-opacity-5 focus:outline-none sm:text-sm"
            >
              <ListboxOption
                v-slot="{ active, selected }"
                v-for="item in items"
                :key="item.name"
                :value="item"
                as="template"
              >
                <li
                  class="px-8"
                  :class="[
                    active ? (customColors ? item.listActive : currentPreset.listActive) : 'text-gray-900',
                    'relative cursor-default select-none py-2 pl-10 pr-4',
                  ]"
                >
                  <span
                    :class="[
                      selected ? 'font-medium' : 'font-normal',
                      'block truncate',
                    ]"
                    >{{ item.name }}</span
                  >
                  <span
                    v-if="selected"
                    class="absolute inset-y-0 left-0 flex items-center pl-3" 
                    :class="[customColors ? item.textColor : currentPreset.text]"
                  >
                    <CheckIcon class="h-5 w-5" aria-hidden="true" />
                  </span>
                </li>
              </ListboxOption>
            </ListboxOptions>
          </transition>
        </div>
      </Listbox>
    </div>
  </template>
  
  <script setup>
  import { ref, computed } from 'vue'
  import {
    Listbox,
    ListboxLabel,
    ListboxButton,
    ListboxOptions,
    ListboxOption,
  } from '@headlessui/vue'
  import { CheckIcon, ChevronUpDownIcon } from '@heroicons/vue/20/solid'
  

  const props = defineProps({
    preset: {
        type: String,
        default: 'vue'
    },
    customColors: {
        type: String, 
        default: false
    }
  });

  const items = [
    { 
        name: 'JavaScript',
        textColor: 'text-yellow-500',
        listActive: 'bg-yellow-100 text-yellow-900'
    },
    { 
        name: 'Typescript',
        textColor: 'text-blue-900 font-bold',
        listActive: 'bg-blue-100 text-blue-900'
    },
    { 
        name: 'React',
        textColor: 'text-blue-400',
        listActive: 'bg-blue-100 text-blue-400'
    },
    { 
        name: 'Vue',
        textColor: 'text-green-400',
        listActive: 'bg-green-100 text-green-400'
    },
    { 
        name: 'Svelte',
        textColor: 'text-orange-400',
        listActive: 'bg-orange-100 text-orange-400'
    },
    { 
        name: 'Angular',
        textColor: 'text-red-400',
        listActive: 'bg-red-100 text-red-400'
    },
  ]

  const presets = {
    jschi: {
        text: 'text-red-500',
        listActive: 'bg-red-100 text-red-900'
    },
    vue: {
        text: 'text-green-400',
        listActive: 'bg-green-100 text-green-900'
    }
  }

  const selectedItem = ref(items[0])
  
  const currentPreset = computed(() => {
    return presets[props.preset]
  })
  </script>


<style scoped>
.slidev-layout li {
    margin-left: 0;
    line-height: 1.8em;
    padding-left: 2.5rem;
}
</style>
  