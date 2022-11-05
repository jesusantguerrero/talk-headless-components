<template>
    <footer 
        v-if="$slidev?.nav.currentLayout !== 'cover'"
        class="absolute bottom-0 left-0 right-0 p-2 flex justify-between"
    >
        <div>
            Jesus Guerrero {{ $slidev }}
        </div>
        <div>
            JS-Chi Meetup Nov 15 2022
        </div>
    </footer>
</template>