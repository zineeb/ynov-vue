<script setup>
const props = defineProps({
  type: {
    type: String,
    default: 'text'
  },
  modelValue: [String, Number],
  placeholder: String,
});
</script>

<template>
  <input :type="type" :value="modelValue" @input="$emit('update:modelValue', $event.target.value)" :placeholder="placeholder" class="input">
</template>

<style scoped>
.input {
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  width: 100%;
  box-sizing: border-box;
}
</style>