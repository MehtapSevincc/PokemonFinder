<template>
  <div
    class="min-h-screen flex items-center justify-center bg-slate-900 text-white"
  >
    <div class="p-6" v-if="details">
      <h2 class="text-4xl font-bold mb-6 capitalize">{{ details.name }}</h2>
      <img
        :src="details.sprites.front_default"
        alt="Pokemon"
        class="mx-auto mb-6 w-[240px] h-[240px]"
      />
      <p class="mb-4">Weight: {{ details.weight }}</p>

      <ul class="text-lg space-y-2">
        <li v-for="stat in details.stats" :key="stat.stat.name">
          <span class="font-medium capitalize">{{ stat.stat.name }}:</span>
          {{ stat.base_stat }}

          <div class="w-full bg-gray-400 rounded h-3 mt-1">
            <div
              class="h-3 bg-gray-100 rounded"
              :style="{ width: stat.base_stat + '%' }"
            ></div>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  props: ["name"],
  data() {
    return {
      details: null,
    };
  },
  mounted() {
    axios.get(`https://pokeapi.co/api/v2/pokemon/${this.name}`).then((res) => {
      this.details = res.data;
    });
  },
};
</script>
