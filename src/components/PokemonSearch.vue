<template>
<div class="w-full relative">
    <Transition name="slide">
        <input type="text" v-model="query" @input="emitSearch" placeholder="Rechercher un Pokémon" class="w-full px-3 py-4 border border-gray-300 rounded-md mb-5 text-base focus:outline-none focus:ring-2 focus:ring-blue-500 transition-all duration-300 hover:shadow-md">
    </Transition>
</div>
</template>

<style>
.slide-enter-active{
    transition: all 0.4s ease-in-out;
}
.slide-leave-active{
    transition: all 0.3s ease-in-out;
}

.slide-enter-from{
    transform: translateY(-20px);
    opacity: 0;
}
.slide-leave-to{
    transform: translateY(20px);
    opacity: 0;
}
</style>

<script setup>
import {ref, Transition} from "vue";

const query = ref('')
const emit = defineEmits(['search'])

const  emitSearch = ()=> {
    emit("search", query.value)
}
</script>