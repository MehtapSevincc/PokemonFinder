<template>
  <div class="p-6" v-if="details">
    <h2 class="text-2x1 font-bold mb-4"></h2>
    <img :src="details.sprites.front_default" alt="Pokemon" class="mb-4" />

    <h3 class="text-x1 font-semibold">İstatistikler</h3>
    <ul class="list-disc pl-5">
     <li v-for="stat in details.stats" :key="stat.stat.name">
    {{ stat.stat.name }} :{{ stat.base_stat }}
     </li>
    </ul>

  </div>
</template>

<script>
import axios from 'axios'

export default {
    props: ['name'],
    data(){
        return {
            details:null
        }
    },
  mounted(){
    axios.get(`https://pokeapi.co/api/v2/pokemon/${this.name}`)
    .then(res => {
        this.details = res.data
    })
  }

}
</script>
