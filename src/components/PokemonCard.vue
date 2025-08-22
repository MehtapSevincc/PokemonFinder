<template>
  <div class="border p-4 rounded shadow w-full max-w-xs mx-auto bg-white">
    <p class="text-lg font-semibold text-center truncate">{{ name }}</p>
  </div>
</template>

<script>
export default {
  name: "PokemonCard",
  props: {
    name: String,
  },
};
</script>
