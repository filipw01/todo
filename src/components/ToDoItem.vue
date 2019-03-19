<template>
  <div>
    <div class="task" @click="openModal">
      <span>{{todo.title}}</span>
      <span class="close" :id="todo.id" @click="removeItem">x</span>
    </div>
    <div v-if="modal" class="modal-background" @click="closeModal"></div>
    <div class="modal" v-if="modal">
      <label for="date">Data</label>
      <input class="modal__input" name="date" type="date" v-model="todo.deadline">
      <br>
      <label for="description">Opis</label>
      <input class="modal__input" name="description" type="text" v-model="todo.description">
      <button class="modal__button" @click="closeModal">Zapisz i zamknij</button>
    </div>
  </div>
</template>
<script>
import redDirective from '../directives/redDirective';

export default {
  directives: { red: redDirective },
  props: {
    todo: {
      type: Object,
      required: true,
    },
  },
  data() {
    return {
      modal: false,
    };
  },
  methods: {
    removeItem(event) {
      this.$emit('remove', event.target.id);
    },
    openModal() {
      this.modal = true;
    },
    closeModal() {
      this.modal = false;
    },
  },
};
</script>
<style scoped>
.task {
  display: flex;
  justify-content: space-between;
  position: relative;
  background-color: rgb(84, 84, 252);
  padding: 5px 10px;
  width: 300px;
  border-radius: 10px;
  margin-bottom: 10px;
  cursor: pointer;
}
.modal {
  background-color: rgb(230, 228, 228);
  position: fixed;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  padding: 50px;
  border-radius: 10px;
  z-index: 2;
}
.modal__input {
  margin: 5px 0 5px 20px;
  border-radius: 10px;
}
.modal__button {
  margin-top: 5px;
  border-radius: 10px;
}
label {
  color: black;
}
.modal-background{
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 1;
}
.close{
  padding: 0 10px;
}
</style>
