<template>
  <div class="todolist">
    <h1>Moja lista</h1>
    <div class="message" v-if="message!==''">
      {{message}}
      <span class="close" @click="dismissMessage">
        <div class="close__bars">
          <span class="close__bar"></span>
          <span class="close__bar"></span>
        </div>
      </span>
    </div>
    <div>
      <input v-model="newTitle" type="text" placeholder="Co chciałbyś zapisać?">
      <button @click="handleSubmit">Dodaj</button>
    </div>
    <div class="tasks">
      <div :key="todo.id" v-for="todo in todos">
        <ToDoItem @remove="removeItem" :todo="todo"/>
      </div>
    </div>
  </div>
</template>
<script>
import ToDoItem from './ToDoItem.vue';

export default {
  data() {
    return {
      newTitle: '',
      todos: [],
      message: '',
    };
  },
  computed: {
    lastItemId() {
      if (this.todos.length === 0) {
        return 1;
      }
      return this.todos[this.todos.length - 1].id;
    },
  },
  methods: {
    handleSubmit() {
      const newTodo = {
        title: this.newTitle,
        deadline: '',
        description: '',
        id: this.lastItemId + 1,
      };
      if (this.newTitle === '') {
        this.message = 'Wpisz coś przed dodaniem';
      } else {
        this.message = 'Dodano zadanie';
        this.todos = [...this.todos, newTodo];
        this.newTitle = '';
      }
    },
    dismissMessage() {
      this.message = '';
    },
    removeItem(id) {
      this.todos = this.todos.filter((todo) => {
        if (todo.id === Number(id)) {
          this.message = 'Usunięto zadanie';
          return false;
        }
        return true;
      });
    },
  },
  components: {
    ToDoItem,
  },
};
</script>
<style scoped>
.todolist {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.message {
  background-color: rgba(251, 255, 27, 0.3);
  padding: 8px 20px;
  border-radius: 5px;
  margin-bottom: 23.45px;
  position: relative;
}
.tasks{
  margin-top: 50px;
}
.close {
  position: absolute;
 background-color: rgb(230, 228, 228);
  border-radius: 50%;
  display: block;
  width: 25px;
  height: 25px;
  top: 0;
  right: 0;
  transform: translate(50%, -50%);
}
.close__bars {
  position: relative;
  height: 100%;
}
.close__bar {
  position: absolute;
  display: block;
  background-color: black;
  width: 15px;
  height: 2px;
  top: 12px;
  left: 6px;
  transform: rotate(45deg);
}
.close__bar:first-child {
  transform: rotate(-45deg);
}
</style>
