<script setup>
import Input from '@/components/atoms/Input.vue';
import Select from '@/components/atoms/Select.vue';
import Button from '@/components/atoms/Button.vue';
import { ref, watch, defineEmits, defineProps } from 'vue';

const emits = defineEmits(['submit']);
const { initialData, todos } = defineProps({
  initialData: Object,
  todos: Array
});

const title = ref('');
const hours = ref('');
const selectedUser = ref('');
const state = ref('');

const userOptions = [
  { value: 'Charles Leclerc', text: 'Charles Leclerc' },
  { value: 'Max Verstappen', text: 'Max Verstappen' },
  { value: 'Lando Norris', text: 'Lando Norris' }
];

const stateOptions = [
  { value: 'A faire', text: 'À faire' },
  { value: 'En cours', text: 'En cours' },
  { value: 'Terminé', text: 'Terminé' }
];

watch(() => initialData, (newVal) => {
  if (newVal) {
    title.value = newVal.title || '';
    hours.value = newVal.hours || '';
    selectedUser.value = newVal.user || userOptions[0].value;
    state.value = newVal.state || stateOptions[0].value;
  }
}, { immediate: true });

const submitForm = () => {
  const hoursNumber = Number(hours.value);

  if (!title.value.trim() || isNaN(hoursNumber) || hoursNumber <= 0 || !selectedUser.value.trim()) {
    alert("Veuillez remplir correctement tous les champs.");
    return;
  }

  const userTasks = todos.filter(todo => todo.user === selectedUser.value);
  const inProgressTasksCount = userTasks.filter(todo => todo.state === 'En cours').length;
  const totalHours = userTasks.reduce((acc, cur) => acc + cur.hours, 0);

  if (inProgressTasksCount >= 3) {
    alert("Cet utilisateur a déjà 3 tâches en cours.");
    return;
  }

  if (totalHours + hoursNumber > 10) {
    alert("L'ajout de cette tâche dépasse le total de 10 heures pour cet utilisateur.");
    return;
  }

  emits('submit', {
    title: title.value,
    hours: hoursNumber,
    user: selectedUser.value,
    state: state.value
  });
};
</script>

<template>
  <form @submit.prevent="submitForm" class="form-container">
    <Input class="input-field" v-model="title" placeholder="Titre de la todo" />
    <Input class="input-field" v-model="hours" type="number" placeholder="Heures estimées" />
    <Select class="select-field" v-model="selectedUser" :options="userOptions" />
    <Select class="select-field" v-model="state" :options="stateOptions" />
    <Button class="submit-button">Soumettre</Button>
  </form>
</template>

<style scoped>
.form-container {
  display: flex;
  flex-direction: column;
  gap: 20px;
}

.input-field, .select-field {
  width: 100%;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.submit-button {
  align-self: flex-end;
  padding: 10px 20px;
  background-color: #5c6bc0;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  margin-top: 20px;
}

.submit-button:hover {
  background-color: #3f51b5;
}
</style>