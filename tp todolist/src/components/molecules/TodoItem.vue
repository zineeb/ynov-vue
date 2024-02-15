<script setup>
import Checkbox from '@/components/atoms/Checkbox.vue';

const props = defineProps({
  id: Number,
  title: String,
  hours: Number,
  user: String,
  state: String,
  isChecked: Boolean
});

const emit = defineEmits(['update:isChecked', 'edit']);

const updateCheck = (newCheckValue) => {
  emit('update:isChecked', { id: props.id, isChecked: newCheckValue });
};

const editTodo = () => {
  emit('edit', props.id);
};
</script>

<template>
  <div class="todo-item">
    <Checkbox :modelValue="isChecked" @update:modelValue="updateCheck"/>
    <span @click="editTodo">{{ title }} - {{ hours }} heures - Responsable : {{ user }} - État : {{ state }}</span>
  </div>
</template>

<style scoped>
.todo-item {
  display: flex;
  align-items: center;
  gap: 10px;
  border: 1px solid #ccc;
  border-radius: 5px;
  padding: 10px;
  margin-bottom: 10px;
  cursor: pointer;
}

.todo-item:hover {
  background-color: #f4f4f4;
}
</style>