<template>
  <div>
    <p>Moja lista</p>

    <div>
      <div v-if="message!==''">
        {{message}}
        <span @click="dismissMessage">x</span>
      </div>
      <input v-model="newTitle" type="text" placeholder="Co chciałbyś zapisać?">
      <button @click="handleSubmit">Dodaj</button>
    </div>
    <div>
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
      todos: [
        {
          id: 1,
          title: 'tytuł',
          deadline: '20 marca',
          description: 'opis',
        },
      ],
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
