<template>
  <div>
    <div v-if="loading">Yükleniyor...</div>

    <div v-else >
      
      <div class="grid grid-cols-2 gap-4">
    <router-link
  v-for="pokemon in paginatedPokemons"
  :key="pokemon.name"
  :to="`/pokemon/${pokemon.name}`"
  class="border p-4 rounded shadow block text-center capitalize hover:bg-slay-800 transition"
>
  {{ pokemon.name }}
</router-link>

      </div>

      
      <div class="mt-4 flex gap-2">
        <button
          @click="prevPage"
          :disabled="currentPage === 1"
          class="bg-gray-300 px-4 py-2 rounded disabled:opacity-50"
        >
          Prev
        </button>

        <button
          @click="nextPage"
          :disabled="currentPage === totalPages"
          class="bg-gray-300 px-4 py-2 rounded disabled:opacity-50"
        >
         Next
        </button>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios'

export default {
  props: ['search'],
  data() {
    return {
      pokemons: [],
      loading: true,
      currentPage: 1,
      itemsPerPage: 12
    }
  },
  computed: {
    filteredPokemons() {
      if (!this.search) return this.pokemons
      const term = this.search.toLowerCase()
      return this.pokemons.filter(p =>
        p.name.toLowerCase().includes(term)
      )
    },
    paginatedPokemons() {
      const start = (this.currentPage - 1) * this.itemsPerPage
      const end = start + this.itemsPerPage
      return this.filteredPokemons.slice(start, end)
    },
    totalPages() {
      return Math.ceil(this.filteredPokemons.length / this.itemsPerPage)
    }
  },
  methods: {
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--
      }
    },
    goToDetail(name) {
        this.$router.push({name:'Detail',params:{name}})
    }
  },
  watch: {
    search() {
      this.currentPage = 1
    }
  },
  mounted() {
    axios.get('https://pokeapi.co/api/v2/pokemon?limit=151&offset=0')
      .then(response => {
        this.pokemons = response.data.results
        this.loading = false
      })
      .catch(error => {
        console.error('API verisi alınamadı:', error)
        this.loading = false
      })
  }
}
</script>
