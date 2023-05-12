<template>
  <div>
    <h1>Character List</h1>
    <ul>
      <li v-for="character in characters" :key="character.id" @click="viewCharacterDetail(character.id)">
        {{ character.name }}
      </li>
    </ul>
  </div>
</template>

<script>
export default {
  data() {
    return {
      characters: [],
    };
  },
  methods: {
    async fetchCharacters() {
      try {
        const response = await fetch('https://rickandmortyapi.com/api/character');
        const data = await response.json();
        this.characters = data.results;
      } catch (error) {
        console.error(error);
      }
    },
    viewCharacterDetail(id) {
      this.$router.push(`/character/${id}`);
    },
  },
  mounted() {
    this.fetchCharacters();
  },
};
</script>

