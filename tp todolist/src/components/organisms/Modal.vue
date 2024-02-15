<template>
  <div class="modal" @click.self="$emit('close')">
    <div class="modal-content">
      <div class="modal-header">
        <slot name="header"></slot>
      </div>
      <div class="modal-body">
        <slot name="body"></slot>
      </div>
      <div class="modal-footer">
        <slot name="footer"></slot>
      </div>
    </div>
  </div>
</template>

<style scoped>
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: rgba(0, 0, 0, 0.5);
}

.modal-content {
  background-color: #fff;
  padding: 20px;
  border-radius: 8px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  width: 50%; /* Modal plus large */
  max-width: 700px;
  min-width: 320px;
  color: black;
}

.modal-header, .modal-body, .modal-footer {
  padding: 10px;
}

.modal-header {
  border-bottom: 1px solid #ccc;
}

.modal-footer {
  border-top: 1px solid #ccc;
  text-align: right;
}

.modal-header h3 {
  text-align: center;
}

.modal input, .modal select {
  border: 1px solid #ccc;
  margin-bottom: 15px;
}
</style>


