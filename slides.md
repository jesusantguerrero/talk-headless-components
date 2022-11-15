---
# theme: default
highlighter: shiki
lineNumbers: true
info: |
  ## Unveiling the power of Headless Components
  Chi.js Meetup.
drawings:
  persist: false
css: unocss
hideInToc: true
layout: cover
---

# Headless Components

<p class="text-xl">
Unveiling the Power of Headless Components in Vue
</p>


<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

---
hideInToc: true
---

# Jesus Guerrero

<div class="grid grid-cols-2 pt-4 items-center">
  <div class=" opacity-80">
  I’m a system engineer and full-stack developer from the Dominican Republic who is passionate about programming in general, <span class="text-green">Vue.js</span>. Building with <span class="text-red">Laravel</span>.

  When I am not coding, I am singing <span class="inline-block text-transparent bg-clip-text bg-gradient-to-r via-yellow from-green to-red">Bob Marley's songs</span> and blues, Running. 

  <div class="mt-12 w-min grid grid-cols-[auto_1fr] gap-2" items-center text-white v-click>
    <mdi-twitter  />
    <div><a href="https://twitter.com/jesusntguerrero" target="_blank">@jesusntguerrero</a></div>
    <mdi-dev-to />
    <div><a href="https://dev.to/jesusantguerrero" target="_blank">jesusantguerrero</a></div>
    <mdi-github />
    <div><a href="https://github.com/jesusantguerrero" target="_blank">jesusantguerrero</a></div>
    <mdi-web />
    <div><a href="https://jesusantguerrero.com" target="_blank">jesusantguerrero.com</a></div>
  </div>

  </div>
  <div>
    <img src="/headshot.jpeg" class="rounded-md h-72 ml-auto">
  </div>
</div>

---
hideInToc: true
---

# Table of Content?

We are going to review the following topics

<!-- <v-clicks>

- **Introduction**
- **What are headless components**
- **Real World Examples of HC**
- **Building a Headless component in Vue**
- **Pros and Cons**
- **Closing**
- **Resources** 

</v-clicks> -->

<Toc />


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
layout: center
class: text-center
hideInToc: true
---

# Headless Components

The problem


<!--
While creating applications you will find yourself either doing the same components with the same logic many times with different User Interface(UI) or installing packages with an opinionated design that have a very different look from the design of your app.

-->

---
hideInToc: true
---

<div class="grid">
</div>
<div class="grid grid-cols-3 gap-3" v-after>
  <div class="text-center">
   <div class="h-38 flex items-center bg-gradient-to-br from-blue-600 to-blue-500 px-10 rounded-md">
     <input class="rounded-md text-sm py-1 px-2" placeholder="Type email" />
    </div>
    <small class="mt-2"> Input</small>
  </div>
  <div class="text-center">
    <div class="h-38 flex items-center bg-gradient-to-br from-purple-500 to-blue-200 px-10 rounded-md">
     <div class="rounded-md text-sm py-1 px-2 bg-white w-full h-32" />
    </div>
    <small> Cards</small>
  </div>
  <div class="text-center">
    <div class="h-38 flex items-center bg-gradient-to-br from-blue-600 to-blue-500 px-10 rounded-md">
     <div class="rounded-full h-10 w-10 bg-white text-sm py-1 px-2 flex items-center justify-center text-blue-300 font-bold">
      JG
     </div>
    </div>
    <small> Avatars </small>
  </div>
</div>
<div class="bg-white/20 px-4 py-1 rounded-md text-xs">
  Overwriting Styles
</div>
<div class="grid grid-cols-3 mt-4 gap-3" v-click>
  <div class="text-center">
    <figure>
      <img src="/step-wizard.webp" class="rounded-md">
    </figure>
    <small class="mt-2"> Step Wizard</small>
  </div>
  <div class="text-center">
    <figure>
      <img src="/file-uploader2.webp" class="rounded-md">
    </figure>
    <h5 class="mt-2"> File Uploader</h5>
  </div>
  <div class="text-center">
    <div class="h-53 flex items-center bg-gradient-to-br from-blue-500 to-blue-200 px-10 rounded-md">
      <ComboboxExample />
    </div>
    <h5 class="mt-2"> Combo Box </h5>
  </div>
</div>

<!-- 
For simple components like inputs, cards, labels, badges, avatars this may be easy but for complex components like ComboBox, Tabs, File Uploader, Date Pickers, Step Wizards this can get complicated if the component wasn't created with UI flexibility in mind
And here is when Headless components come to the rescue.

 -->

---
preload: false
clicks: 4
---

# What are headless components?
<v-click>
<div class="grid grid-cols-3">
  <div class="text-center">
    <h4> Structure</h4>
  </div>
  <div class="text-center">
    <h4> Logic & Behavior</h4>
  </div>
  <div class="text-center">
    <h4> Styles </h4>
  </div>
</div>

<img src="/component-structure.png" class="rounded-md mt-5" />
</v-click>


  <div
    v-motion
    v-click
    class="rounded-md bg-green-400 text-white w-57 h-26 py-4 px-1 text-sm"
    :initial="{ x:35, y: 40, opacity: 0}"
    :enter="{ y: -125, x: 560, opacity: 1}">

  <div v-click="4">

    - User Defined UI
    - Expose State Values
    - Expose Controls (functions)
      
  </div>
      
  </div>

<!-- 

In plain words, headless components are the ones that handle the Structure, logic and behavior separated from the UI, giving the decision of how the component looks to like to the developer.

can expose values and functions (state and controls) that will allow a child component to control certain parts of it and make UI decisions based on a state value. In other words, they are not attached to the UI but serves as support.

-->

---

# Characteristics, Pros and Cons?

<div class="grid grid-cols-2 gap-2">

<div>
<v-after>

- Unstyled

</v-after>

<v-clicks>

- Accessible components
- Design Systems (sharing components between design systems)
- Create abstraction for components that behave in the same way
- No need to override styles
- integrate with multiple style approaches

</v-clicks>

</div>


<SimpleCard class="items-center bg-gradient-to-br from-blue-500 to-blue-200 mt-10">
  <v-click at="0">
      <ComboboxExample />
  </v-click>

  <v-click at="2">
    <ComboboxExample preset="jschi" />
  </v-click>

  <v-click at="5" >
    <ComboboxExample :custom-colors="true" />
  </v-click>

</SimpleCard>

</div>

<!-- 

Thats what we call Unstyled

Eg. 

-->
---
layout: center
class: text-center
hideInToc: true
---

# Building our own HC

With Vue and The Composition API
---
layout: iframe
url: https://tally.so/r/3xJoyn
class: my-cool-content-on-the-right
---

# Building a Headless Component

---
hideInToc: true
---

# Building a Headless Component

<div>

  Requirements:

  - The user can specify the count of how many stars should display
  - Should expose the selected state
  - Should expose the covered state

  To build this component we are going to use TailwindCSS for styling and Vue 3

</div>

<div 
  class="absolute top-20 left-13 w-250"  
  v-click="1"
  v-motion
  :initial="{ x: -35, y: -40, opacity: 0}"
  :enter="{ y: 0, x: 0, opacity: 1}"
>

```html {all|all|4-7|8-9|12-14|17-19|21-23|all}
<script setup>
import { ref, computed } from "vue";

const props = defineProps({
  modelValue: { type: Number },
  count: { type: Number }
});
const lastHoveredItem: ref(0);
const range: computed(() => [...Array(props.count).keys()]);

// state functions
function isCovered(itemNumber) {
  return props.modelValue >= itemNumber 
  || lastHoveredItem.value >= itemNumber;
}

function isSelected(itemNumber) {
  return props.modelValue == itemNumber;
}

function setHovered(itemNumber) {
  lastHoveredItem.value = itemNumber;
}
```

</div>


---
hideInToc: true
---

# Building a BareRate Component

```html {all|3-5|6-9|all}
<template>
  <div>
    <slot
        v-for="index in range" 
        :key="index" 
        :item-number="index+1"
        :selected="isSelected(index+1)"
        :covered="isCovered(index+1)"
        :set-hovered="setHovered"
    />
  </div>
</template>
```

---
hideInToc: true
title: Using our headless component
level: 2
---

# Using our components

```html {all|3|5|7-9|11|13|all}
<BareRate 
  v-model="rating" 
  :count="5" 
  class="space-x-2 cursor-pointer" 
  v-slot:default="{ selected, covered, itemNumber, setHovered }">
    <button 
      @click="rating=itemNumber" 
      @mouseover="setHovered(itemNumber)"
      @mouseout="setHovered(0)"
      class="font-bold text-gray-400 transition transform cursor-pointer hover:text-yellow-400 hover:scale-110" 
      :class="[selected || covered ? 'text-yellow-500': 'text-gray-400']"
    > 
      <mdi-star />
  </button>
</BareRate>
```

<!-- ./components/Rate.vue -->
<Rate />

---
class: px-20
hideInToc: true
---

# Using our components: improved Rate

```html
<BareRate 
  v-model="rating" 
  :count="5" 
  class="space-x-2 cursor-pointer" 
  v-slot:default="{ selected, covered, itemNumber }">
    <BareRateButton 
      :item-number="itemNumber"
      class="font-bold transition transform cursor-pointer hover:text-yellow-400 hover:scale-110" 
      :class="[selected || covered ? 'text-yellow-500': 'text-gray-400']"
    > 
      <i class="fa fa-star" > </i>
  </BareRatebutton>
</BareRate>
```

<!-- ./components/NewRate.vue -->
<NewRate />

---
hideInToc: true
title: Refactoring our headless component
level: 2
---

# Refactoring our Headless Component

<article class="flex space-x-2 justify-between">
<div>

```html {all|3|13-15|17-21|all}
<!-- BareRate.vue -->
<script setup>
import { ref, computed, provide } from "vue";
...

// state functions
function isCovered(itemNumber) { ... }

function isSelected(itemNumber) { ... }

function setHovered(itemNumber) { ... }

const setSelected = (itemNumber) => {
  emit('update:modelValue', itemNumber)
}

provide('controls', {
  setHovered,
  setSelected
})
```

</div>

<div>

```html {all|3|5-7|9|all}
<!-- BareRateButton.vue -->
<script setup>
  import { inject } from "vue"

  defineProps({
    itemNumber: { type: Number }
  })

  const { setSelected, setHovered } = inject('controls')
</script>
```

```html {2|3-5|5-7|all}
 <button
    @click="setSelected(itemNumber)" 
    @mouseover="setHovered(itemNumber)"
    @mouseout="setHovered(0)">
      <slot>
          {{ itemNumber }}
      </slot>
  </button>
```
</div>
</article>


---
hideInToc: true
title: Reusing the Rate component for Scale
level: 2
---

# Reusing our headless to build an Scale

```html {all|3|5|8-9|all}
<BareRate 
  v-model="scale" 
  :count="10" 
  class="space-x-2 cursor-pointer" 
  v-slot:default="{ selected, itemNumber }">
  <BareRateButton
    :item-number="itemNumber"
    class="px-3 py-0.5 font-bold border bg-white/5 border-gray-400 rounded-lg cursor-pointer hover:text-red-300" 
    :class="{'text-red-300 border-red-300 shadow-md ring ring-red-300': selected}"
  />
</BareRate>
```
<div>
<h4 class="mt-12 mb-1 font-bold text-white">How likely would you recommend this js-chi meetup to your friends?</h4>
<BareRate v-model="scale" :count="10" class="space-x-2 cursor-pointer" v-slot:default="{ selected, covered, itemNumber }">
  <BareRateButton 
      :item-number="itemNumber"
      class="px-3 py-0.5 font-bold border bg-white/5 border-gray-400 transition transform rounded-lg cursor-pointer hover:text-red-300" 
      :class="{'text-red-300 border-red-300 shadow-md ring ring-red-300': selected}"
  />
</BareRate>
</div>

<script setup> 
  import { ref } from "vue"

  const scale = ref(0)
</script>

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
title: Conclusion
level: 2 
---

# Wrapping Up

- Provide a way to reuse the logic with customizable the UI.

- Good for sharing complex components across projects.

- Requires wrapper components to use your customized UI across the app