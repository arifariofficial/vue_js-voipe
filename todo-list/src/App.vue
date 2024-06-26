<template>
  <div id="app">
    <h1>To-Do Lista</h1>
    <todo-form @todo-added="addToDo"></todo-form>
    <h2 id="list-summery" ref="listSummary" tabindex="-1">{{ listSummary }}</h2>
    <ul class="stack-large">
      <li v-for="item in TodoItems" :key="item.id">
        <todo-item
          :label="item.label"
          :done="item.done"
          :id="item.id"
          @checkbox-changed="($event) => updateDoneStatus(item.id)"
          @item-deleted="($event) => deleteToDo(item.id)"
          @item-edited="($event) => editToDo(item.id, $event)"
        ></todo-item>
      </li>
    </ul>
  </div>
</template>

<script>
  import TodoItem from "./components/ToDoItem.vue";
  import uniqueId from "lodash.uniqueid";
  import TodoForm from "./components/ToDoForm.vue";

  export default {
    name: "App",
    components: {
      TodoItem,
      TodoForm,
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
    methods: {
      addToDo(toDoLabel) {
        this.TodoItems.push({ id: uniqueId("todo-"), label: toDoLabel, done: false });
      },
      updateDoneStatus(toDoId) {
        const todDoUpdate = this.TodoItems.find((item) => item.id === toDoId);
        todDoUpdate.done = !todDoUpdate.done;
      },
      deleteToDo(toDoId) {
        const itemIndex = this.TodoItems.findIndex((item) => item.id === toDoId);
        this.TodoItems.splice(itemIndex, 1);
        this.$refs.listSummary.focus();
      },
      editToDo(toDoId, newlabel) {
        const toDoToEdit = this.TodoItems.find((item) => item.id === toDoId);
        toDoToEdit.label = newlabel;
      },
    },
    computed: {
      listSummary() {
        const numberFinishedItems = this.TodoItems.filter((item) => item.done).length;
        return `${numberFinishedItems} out of ${this.TodoItems.length} items completed`;
      },
    },
  };
</script>

<style>
  .stack-small > * + * {
    margin-top: 1.25rem;
  }
  .stack-large > * + * {
    margin-top: 2.5rem;
  }
  @media screen and (min-width: 550px) {
    .stack-small > * + * {
      margin-top: 1.4rem;
    }
    .stack-large > * + * {
      margin-top: 2.8rem;
    }
  }
  /* End global styles */

  @media screen and (min-width: 550px) {
    #app {
      padding: 4rem;
    }
  }
  #app > * {
    max-width: 50rem;
    margin-left: auto;
    margin-right: auto;
  }
  #app > form {
    max-width: 100%;
  }
  #app h1 {
    display: block;
    min-width: 100%;
    width: 100%;
    text-align: center;
    margin: 0;
    margin-bottom: 1rem;
  }
</style>
