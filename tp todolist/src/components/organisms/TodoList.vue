<script setup>
import { computed, ref } from 'vue';
import TodoItem from '@/components/molecules/TodoItem.vue';
import TodoForm from '@/components/molecules/TodoForm.vue';

const todos = ref([]);
const filter = ref('all');
let nextTodoId = ref(todos.value.length + 1);
const editableTodo = ref(null);

const filteredTodos = computed(() => {
  switch (filter.value) {
    case 'all':
      return todos.value;
    case 'completed':
      return todos.value.filter(todo => todo.state === 'Terminé');
    case 'active':
      return todos.value.filter(todo => todo.state !== 'Terminé');
    default:
      return todos.value;
  }
});

function handleFormSubmit(todoData) {
  if (editableTodo.value) {
    const index = todos.value.findIndex(todo => todo.id === editableTodo.value.id);
    if (index !== -1) {
      todos.value[index] = { ...todos.value[index], ...todoData };
    }
    editableTodo.value = null; // Reset après édition
  } else {
    todos.value.push({ id: nextTodoId.value++, ...todoData, isChecked: false });
  }
}

function editTodo(id) {
  const todo = todos.value.find(todo => todo.id === id);
  if (todo) {
    editableTodo.value = { ...todo };
  }
}

function updateCheck({ id, isChecked }) {
  const todo = todos.value.find(todo => todo.id === id);
  if (todo) {
    todo.isChecked = isChecked;
  }
}
</script>

<template>
  <div>
    <TodoForm @submit="handleFormSubmit" :initialData="editableTodo"/>
    <div class="todo-list">
      <div v-for="todo in filteredTodos" :key="todo.id" class="todo-item">
        <TodoItem
            :id="todo.id"
            :title="todo.title"
            :hours="todo.hours"
            :user="todo.user"
            :state="todo.state"
            :isChecked="todo.isChecked"
            @edit="editTodo"
            @update:isChecked="updateCheck($event)"
        />
      </div>
    </div>
  </div>
</template>

<style scoped>
.todo-list {
  display: flex;
  flex-direction: column;
}
.todo-item {
  margin-bottom: 10px;
}
</style>