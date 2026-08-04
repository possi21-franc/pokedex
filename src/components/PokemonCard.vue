<template>
<div class="roundde-lg border border-gray-300 p-4 text-center bg-white shadow-md hover:shadow-lg transition-all duration-300 hover:border-blue-500">
    <img :src="pokemon.image || fallbackImage" :alt="pokemon.name" class="w-24 h-24 mx-auto transition-transform duration-500 hover:rotate-3 hover:scale-110">
    <h2 class="text-xl font-bold mt-2 text-gray-800">{{ pokemon.name }}</h2>

    <div class="mt-2 space-y-1">
        <p class="text-gray-700 transition-all duration-200 hover:text-blue-500"> ⚔️ Attaque: {{pokemon.stats.HP}}</p>
        <p class="text-gray-700 transition-all duration-200 hover:text-red-500"> 🛡️ Défense: {{pokemon.stats.attack}}</p>
        <p class="text-gray-700 transition-all duration-200 hover:text-green-500">⚡Combat: {{pokemon.stats.defense}}</p>
       
    <!-- Bouton téléchargement -->
    <button
      @click="downloadImage(pokemon.image, pokemon.name)"
      class="bg-blue-500 hover:bg-blue-600 text-white font-medium py-2 px-4 rounded shadow transition-colors duration-200  items-center gap-2 hover:cursor-pointer"
    >
      
      Télécharger l'image
    </button>
    </div>
</div>
</template>

<script setup>

import { defineProps } from "vue";

const fallbackImage = "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/0.png";

defineProps({
    pokemon:Object
})


function downloadImage(url, name) {
  fetch(url)
    .then(res => res.blob())
    .then(blob => {
      const a = document.createElement('a');
      a.href = URL.createObjectURL(blob);
      a.download = `${name}.png`; // nom du fichier
      a.click();
      URL.revokeObjectURL(a.href); // nettoyage
    })
    .catch(err => console.error('Erreur téléchargement', err));
}
</script>