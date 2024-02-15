<script setup>
const { modelValue } = defineProps({
  modelValue: Boolean
});
</script>

<template>
  <input type="checkbox" :checked="modelValue" @change="$emit('update:modelValue', $event.target.checked)">
</template>