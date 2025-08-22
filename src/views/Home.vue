<template>
  <div class="p-6 max-w-3xl mx-auto">
    <h1 class="text-3xl font-bold mb-7">Search For Your Pokemon</h1>
    <label class="block text-lg font-medium mb-2" for="search"
      >Pokemon Name</label
    >
    <div class="mb-6">
      <SearchBar v-model="searchTerm" />
    </div>
    <PokemonList :search="searchTerm" />
  </div>
</template>

<script>
import SearchBar from "../components/SearchBar.vue";
import PokemonList from "../components/PokemonList.vue";

export default {
  components: {
    SearchBar,
    PokemonList,
  },

  data() {
    return {
      searchTerm: "",
    };
  },
};
</script>
