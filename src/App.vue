<template>
  <div>
    <h1 class="title">Personagens</h1>
    <ul class="characters">
      <li
        v-for="character in characters"
        :key="character.id"
        class="character-item"
      >
        <img
          :src="character.image"
          :alt="character.name"
          width="200"
          height="200"
          class="character-image"
        />
        <h2 class="character-name">{{ character.name }}</h2>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import { fetchCharacters } from "./Services/rickAndMortyApi";
import { type Character } from "./Types/rickAndMortyTypes";

const characters = ref<Character[]>([]);

onMounted(async () => {
  try {
    characters.value = await fetchCharacters();
  } catch (error) {
    console.error("Erro ao buscar Personagens:", error);
  }
});
</script>

<style scoped>
.title {
  text-align: center;
  margin-bottom: 20px;
}

.characters {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

.character-item {
  margin: 10px;
}

.character-image {
  border-radius: 10px;
}

.character-name {
  text-align: center;
  margin-top: 10px;
}
</style>
