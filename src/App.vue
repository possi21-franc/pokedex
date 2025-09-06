<template>
  <div class="max-w-6xl mx-auto py-12 px-4">
    <div class="flex justify-center mb-6">
      <PokemonSearch @search="searchPokemon" />
    </div>

    <!-- Loader -->
    <div v-if="loading" class="flex justify-center mb-6">
      <div class="animate-spin rounded-full h-12 w-12 border-t-2 border-blue-500 border-b-2"></div>
      <p class="ml-3">Chargement...</p>
    </div>

    <!-- Aucun Pokémon trouvé -->
    <div v-else-if="filteredPokemons.length === 0" class="text-center">
      <p class="text-xl text-gray-500">
        Aucun Pokémon trouvé pour votre recherche
      </p>
    </div>

    <!-- Liste des Pokémon -->
    <Transition name="fade">
      <PokemonList
        
        :pokemons="filteredPokemons"
      >
        <template #default="{ pokemon }">
          <PokemonCard :pokemon="pokemon" />
        </template>
      </PokemonList>
    </Transition>
  </div>
</template>

<style>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease-in-out;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
}
</style>

<script setup>
import { ref, onMounted, computed } from "vue";
import PokemonList from "./components/PokemonList.vue";
import PokemonCard from "./components/PokemonCard.vue";
import PokemonSearch from "./components/PokemonSearch.vue";

const pokemons = ref([]);
const searchQuery = ref("");
const loading = ref(true);

onMounted(async () => {
  try {
    const response = await fetch("https://pokebuildapi.fr/api/v1/pokemon");
    pokemons.value = await response.json();
    console.log('Premier pokémon:', pokemons.value[0]); // AJOUTEZ CETTE LIGNE
  } catch (error) {
    console.error("Error fetching data", error);
  } finally {
    loading.value = false;
  }
});

const filteredPokemons = computed(() => {
  if (!searchQuery.value) return pokemons.value;
  return pokemons.value.filter((p) =>
    p.name.toLowerCase().includes(searchQuery.value.toLowerCase())
  );
});

const searchPokemon = (query) => {
  searchQuery.value = query;
};
</script>
