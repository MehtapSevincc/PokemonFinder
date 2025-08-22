<template>
  <input
    type="text"
    :value="modelValue"
    @input="$emit('update:modelValue', $event.target.value)"
    placeholder="Clefable,Pikachu,etc."
    class="w-50 border px-4 py-2 rounded text-slate-950"
  />
</template>

<script>
export default {
  name: "SearchBar",
  props: {
    modelValue: String,
  },
};
</script>
