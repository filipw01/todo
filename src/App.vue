<template>
  <div id="app">
    <ToDoList/>
  </div>
</template>

<script>
import ToDoList from './components/ToDoList.vue';

export default {
  name: 'app',
  components: {
    ToDoList,
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Open+Sans');
html {
  background-color: rgb(33, 42, 61);
  font: 20px 'Open Sans', sans-serif;
  color: rgb(230, 228, 228);
}
h1 {
  font-size: 35px;
}
input{
  border-radius: 10px 0 0 10px;
  border: none;
  height: 35px;
  text-indent: 10px;
  font: 18px 'Open Sans', sans-serif;
}
button{
  height: 37px;
  border-radius: 0 10px 10px 0;
  border: none;
  color: white;
  padding: 0 15px;
  background-color: rgb(84, 84, 252);
  font: 18px 'Open Sans', sans-serif;
  cursor: pointer;
}
.close{
  cursor: pointer;
}
</style>
