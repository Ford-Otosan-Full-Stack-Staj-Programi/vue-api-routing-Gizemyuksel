<template>
  <div v-if="character">
    <h2>{{ character.name }}</h2>
    <img :src="character.image" :alt="character.name" />
    <p>Species: {{ character.species }}</p>
    <p>Status: {{ character.status }}</p>
    <p>Gender: {{ character.gender }}</p>
  </div>
  <div v-else>
    <p>Loading character...</p>
  </div>
</template>

<script>
export default {
  data() {
    return {
      character: null,
    };
  },
  methods: {
    async fetchCharacter() {
      try {
        const response = await fetch(`https://rickandmortyapi.com/api/character/${this.$route.params.id}`);
        const data = await response.json();
        this.character = data;
      } catch (error) {
        console.error(error);
      }
    },
  },
  mounted() {
    this.fetchCharacter();
  },
};
</script>
