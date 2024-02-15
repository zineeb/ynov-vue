<script setup>
import { ref, computed } from 'vue';
import Button from '@/components/atoms/Button.vue';
import Checkbox from '@/components/atoms/Checkbox.vue';
import Modal from '@/components/organisms/Modal.vue';
import TodoForm from '@/components/molecules/TodoForm.vue';

const todos = ref([]);
const filterState = ref('Tous');
const showModalTodo = ref(false);
const editingTodoId = ref(null);
const editableTodo = ref({});

const setFilter = (state) => {
  filterState.value = state;
};

const handleFormSubmit = (todoData) => {
  if (editingTodoId.value) {
    const index = todos.value.findIndex(todo => todo.id === editingTodoId.value);
    todos.value[index] = { ...todos.value[index], ...todoData };
  } else {
    todos.value.push({ ...todoData, id: Date.now(), isChecked: false });
  }
  closeModal();
};

const editTodo = (todoId) => {
  const todo = todos.value.find(todo => todo.id === todoId);
  if (todo) {
    editingTodoId.value = todoId;
    editableTodo.value = { ...todo };
    showModalTodo.value = true;
  }
};

const deleteSelectedTodos = () => {
  todos.value = todos.value.filter(todo => !todo.isChecked);
};

const closeModal = () => {
  showModalTodo.value = false;
  editingTodoId.value = null;
  editableTodo.value = {};
};

const totalTodos = computed(() => { return filteredTodos.value.length; });
const selectedTodosCount = computed(() => todos.value.filter(todo => todo.isChecked).length);

const filteredTodos = computed(() => {
  switch (filterState.value) {
    case 'A faire':
      return todos.value.filter(todo => todo.state === 'A faire');
    case 'En cours':
      return todos.value.filter(todo => todo.state === 'En cours');
    case 'Terminé':
      return todos.value.filter(todo => todo.state === 'Terminé');
    default:
      return todos.value;
  }
});

const prepareEditTodo = (todoId) => {
  editTodo(todoId);
  showModalTodo.value = true;
};
</script>

<template>
  <div class="dashboard">
    <h1>Gestion des tâches</h1>

    <Button @click="showModalTodo = true" class="add-todo">Ajouter une todo</Button>

    <div class="filters">
      <Button @click="setFilter('Tous')">Toutes les tâches</Button>
      <Button @click="setFilter('A faire')">À faire</Button>
      <Button @click="setFilter('En cours')">En cours</Button>
      <Button @click="setFilter('Terminé')">Terminées</Button>
    </div>

    <div>
      Total de tâches : {{ totalTodos }}<br>
      Tâches sélectionnées : {{ selectedTodosCount }}
    </div>

    <div class="todos">
      <div v-for="(todo, index) in filteredTodos" :key="index" class="todo-item">
        <Checkbox v-model="todo.isChecked" />
        <span @click="prepareEditTodo(todo.id)">
        {{ todo.title }} - {{ todo.hours }} heures - Responsable : {{ todo.user }} - État : {{ todo.state }}
      </span>
      </div>
    </div>

    <Button @click="deleteSelectedTodos" class="delete-button">Supprimer les tâches sélectionnées</Button>

    <Modal v-if="showModalTodo" @close="closeModal">
      <template #header>
        <h3>{{ editingTodoId ? 'Éditer la todo' : 'Ajouter une todo' }}</h3>
      </template>
      <template #body>
        <TodoForm @submit="handleFormSubmit" :initialData="editableTodo" :todos="todos" />
      </template>
    </Modal>
  </div>
</template>

<style scoped>
.dashboard {
  font-family: 'Arial', sans-serif;
  padding: 20px;
  max-width: 800px;
  margin: 40px auto;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  border-radius: 8px;
}

.add-todo {
  margin-bottom: 20px;
}

.filters button {
  margin-right: 10px;
  margin-bottom: 20px;
}

.todos button {
  margin-right: 0.5rem;
  margin-bottom: 0.5rem;
}

input[type="text"],
input[type="number"],
select {
  margin-bottom: 20px;
  width: calc(100% - 40px);
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.delete-button {
  background-color: #ef233c;
  color: white;
  padding: 10px 20px;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 20px;
}

.delete-button:hover {
  background-color: #d90429;
}

.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 0.5rem;
}

.todo-item span {
  flex-grow: 1;
  margin-left: 0.5rem;
  cursor: pointer;
}
</style>