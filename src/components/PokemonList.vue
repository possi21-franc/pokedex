<template>
  <TransitionGroup
    name="list"
    tag="div"
    class="grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-4 gap-4 p-5"
  >
    <div
      v-for="pokemon in pokemons"
      :key="pokemon.id"
      class="transform hover:scale-105 transition-all duration-200"
    >
      <slot :pokemon="pokemon"></slot>
    </div>
  </TransitionGroup>
</template>

<script setup>
defineProps({
  pokemons: {
    type: Array,
    required: true
  }
})
</script>

<style>
.list-move,
.list-enter-active,
.list-leave-active {
  transition: all 0.3s ease-in-out;
}

.list-enter-from,
.list-leave-to {
  opacity: 0;
  transform: translateY(20px);
}
</style>
