<template>
  <button class="button" @click="$emit('click')">
    <slot></slot>
  </button>
</template>

<style scoped>
.button {
  background-color: #9a8c98;
  color: white;
  padding: 10px 15px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-weight: bold;
}

.button:hover {
  background-color: #837780;
}
</style>