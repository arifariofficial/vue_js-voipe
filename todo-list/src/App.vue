<template>
  <div id="app">
    <h1>To-Do Lista</h1>
    <ul>
      <li v-for="item in TodoItems" :key="item.id">
        <todo-item :label="item.label" :done="item.done"></todo-item>
      </li>
    </ul>
  </div>
</template>

<script>
  import TodoItem from "./components/ToDoItem.vue";
  import uniqueId from "lodash.uniqueid";

  export default {
    name: "App",
    components: {
      TodoItem,
    },
    data() {
      return {
        TodoItems: [
          { id: uniqueId("todo-"), label: "Opiskele Vue.js", done: false },
          { id: uniqueId("todo-"), label: "Tee eka vue.js app", done: true },
          { id: uniqueId("todo-"), label: "Pida kivaaa", done: true },
          { id: uniqueId("todo-"), label: "Tee to-do lista", done: false },
          { id: uniqueId("todo-"), label: "Ota opntopisteet kotiin", done: false },
        ],
      };
    },
  };
</script>

<style>
  #app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>
