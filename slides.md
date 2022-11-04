---
theme: default
background: https://source.unsplash.com/collection/94734566/1920x1080
class: 'text-center'
highlighter: shiki
lineNumbers: true
info: |
  ## Unveiling the power of Headless Components
  Chi.js Meetup.
drawings:
  persist: false
css: unocss
---

# Unveiling the Power of Headless Components in Vue
Jesus Guerrero

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---

# Jesus Guerrero

<div class="grid grid-cols-2 pt-4 items-center">
  <div>
  I’m a system engineer and full-stack developer from the Dominican Republic who is passionate about programming in general, web development and Vue.js. Building with Laravel.

  When I am not coding, I am singing Bob Marley's songs and blues, Running. 
  
  [@jesusntguerrero](https://twitter.com/jesusntguerrero) <br>
  [jesusantguerrero](https://github.com/jesusantguerrero) <br>
  [jesusantguerrero.com](https://jesusantguerrero.com) <br>
  </div>
  <div>
    <img src="/headshot.jpeg" class="rounded-md h-72 ml-auto">
  </div>
</div>

---

# Table of Content?

We are going to review the following topics

<v-clicks>

- **Introduction**
- **What are headless components**
- **Real World Examples of HC**
- **Building a Headless component in Vue**
- **Pros and Cons**
- **Closing**
- **Resources** 

</v-clicks>


<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h1 {
  background-color: #2B90B6;
  background-image: linear-gradient(45deg, #4EC5D4 10%, #146b8c 20%);
  background-size: 100%;
  -webkit-background-clip: text;
  -moz-background-clip: text;
  -webkit-text-fill-color: transparent;
  -moz-text-fill-color: transparent;
}
</style>

---

# Introduction

Hover on the bottom-left corner to see the navigation's controls panel, [learn more](https://sli.dev/guide/navigation.html)

<div>

</div>
<!-- 
  For simple components like inputs, cards, labels, badges, avatars this may be easy but for complex components like ComboBox, Tabs, File Uploader, Date Pickers this can get complicated

  And here is when Headless components shines.
 -->

---

# What are headless component?

<v-clicks>

- Unstyled
- Accessible components
- Design Systems (sharing components between design systems)
- Create abstraction for components that behave in the same way
- No need to override styles
- integrate with multiple style approaches

</v-clicks>

---

# Resources
<div class="flex justify-between space-x-8">
<div class="w-full">
  <img src="/headlessui.png" class="rounded-md w-full" />

  - [Headless UI](https://headlessui.com/)
</div>
<div class="w-full">
  <img src="/radix.png"  class="rounded-md w-full" />

  - [Radix](https://www.radix-ui.com/)
</div>
</div>

<v-clicks>



</v-clicks>

<!-- 
  Headless components are normal components 

  https://www.radix-ui.com/
  - unstyled,
  - accessible components
  - Design Systems (specially sharing components between design systems)
  - Create abstraction for components that behave in the same way
  - No need to override styles / avoid specificity wars
  - integrate with css-modules/tailwindcss or whatever css solution
  - 
 -->
---

# Building a BareRate Component

```html {all|2|1-6|9|all}
// BareRate.vue
<template>
  <div>
    <slot
        v-for="current in range" 
        :key="current" 
        :current="current+1"
        :selected="isSelected(current+1)"
        :covered="isCovered(current+1)"
        :set-hovered="setHovered"
    >
        {{ current }}
    </slot>
  </div>
</template>
```

---

```html {all|5-8|10-14|15-22|23-25|27-30|all}
// BareRate.vue
<script setup>
import { ref, computed, reactive } from "vue";

const props = defineProps({
  modelValue: { type: Number },
  count: { type: Number }
});

const state = reactive({
  hoveredIndex: 0,
  range: computed(() => {
    return [...Array(props.count).keys()];
  }),
})

// state functions
function isCovered(current) {
  return props.modelValue >= current 
  || state.hoveredIndex.value >= current;
}

function isSelected(current) {
  return props.modelValue == current;
}

function setHovered(current) {
  state.hoveredIndex.value = current;
}
```

---

# Using our components

```html
<BareRate 
  v-model="rating" 
  :count="5" 
  class="space-x-2 cursor-pointer" 
  v-slot:default="{ selected, covered, current, setHovered }">
    <button 
      @click="rating=current" 
      @mouseover="setHovered(current)"
      @mouseout="setHovered(0)"
      class="font-bold text-gray-400 transition transform cursor-pointer hover:text-yellow-400 hover:scale-110" 
      :class="[(selected || covered) ? 'text-yellow-500': 'text-gray-400']"
    > 
      <i class="fa fa-star" > </i>
  </button>
</BareRate>
```

<!-- ./components/Rate.vue -->
<Rate />
---
class: px-20
---

# Using our components

```html
<BareRate 
  v-model="rating" 
  :count="5" 
  class="space-x-2 cursor-pointer" 
  v-slot:default="{ selected, covered, current }">
    <BareRateButton 
      :current="current"
      class="font-bold text-gray-400 transition transform cursor-pointer hover:text-yellow-400 hover:scale-110" 
      :class="[(selected || covered) ? 'text-yellow-500': 'text-gray-400']"
    > 
      <i class="fa fa-star" > </i>
  </BareRatebutton>
</BareRate>
```

<!-- ./components/NewRate.vue -->
<NewRate />

---

# Reusing our headless to build a new component

<v-click>

```html
<BareRate 
  v-model="scale" 
  :count="10" 
  class="space-x-2 cursor-pointer" 
  v-slot:default="{ selected, covered, current }">
    <BareRateButton 
      :current="current"
      class="font-bold text-gray-400 transition transform cursor-pointer hover:text-yellow-400 hover:scale-110" 
      :class="[(selected) ? 'text-yellow-500': 'text-gray-400']"
    />
</BareRate>
```
<BareRate 
  v-model="scale" 
  :count="10" 
  class="space-x-2 cursor-pointer" 
  v-slot:default="{ selected, covered, current }">
    <BareRateButton 
      :current="current"
      class="font-bold text-gray-400 transition transform cursor-pointer hover:text-yellow-400 hover:scale-110" 
      :class="[selected ? 'text-yellow-500': 'text-gray-400']"
    />       
</BareRate>

</v-click>

<script setup> 
  import { ref } from "vue"

  const scale = ref(0)
</script>
