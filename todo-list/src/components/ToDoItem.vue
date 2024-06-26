<template>
  <div class="stack-small">
    <div class="custom-checkbox" v-if="!isEditing">
      <input
        type="checkbox"
        class="checkbox"
        :id="id"
        :checked="isDone"
        @change="($event) => $emit('checkbox-changed')"
      />
      <label :for="id" class="checkbox-label">{{ label }}</label>
    </div>
    <to-do-item-edit-form
      v-if="isEditing"
      :id="id"
      :label="label"
      @item-edited="itemEdited"
      @editCancelled="editCancelled"
    ></to-do-item-edit-form>
    <div class="btn-group">
      <button type="button" class="btn" ref="editButton" @click="toggleToItemEditForm">
        Muokka
        <span class="visually-hidden">{{ label }}</span>
      </button>
      <button class="btn btn_danger" type="button" @click="deleteToDo">
        Delete
        <span class="visually-hidden">{{ label }}</span>
      </button>
    </div>
  </div>
</template>

<script>
  import ToDoItemEditForm from "./ToDoItemEditForm.vue";
  export default {
    components: { ToDoItemEditForm },
    props: {
      label: { required: true, type: String },
      done: { required: true, type: Boolean },
      id: { required: true, type: String },
    },
    data() {
      return {
        isDone: this.done,
        isEditing: false,
      };
    },
    methods: {
      deleteToDo() {
        this.$emit("item-deleted");
      },
      toggleToItemEditForm() {
        this.isEditing = true;
      },
      itemEdited(newLabel) {
        this.$emit("item-edited", newLabel);
        this.isEditing = false;
      },
      editCancelled() {
        this.isEditing = false;
      },
    },
  };
</script>

<style scoped>
  .custom-checkbox > .checkbox-label {
    font-family: Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-weight: 400;
    font-size: 16px;
    font-size: 1rem;
    line-height: 1.25;
    color: #0b0c0c;
    display: block;
    margin-bottom: 5px;
  }

  .custom-checkbox > .checkbox {
    font-family: Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    font-weight: 400;
    font-size: 16px;
    font-size: 1rem;
    line-height: 1.25;
    box-sizing: border-box;
    width: 100%;
    height: 40px;
    height: 2.5rem;
    margin-top: 0;
    padding: 5px;
    border: 2px solid #0b0c0c;
    border-radius: 0;
    appearance: none;
  }

  .custom-checkbox > input:focus {
    outline: 3px dashed #fd0;
    outline-offset: 0;
    box-shadow: inset 0 0 0 2px;
  }

  .custom-checkbox {
    font-family: Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    font-weight: 400;
    font-size: 1.6rem;
    line-height: 1.25;
    display: block;
    position: relative;
    min-height: 40px;
    margin-bottom: 10px;
    padding-left: 40px;
    clear: left;
  }

  .custom-checkbox > input[type="checkbox"] {
    -webkit-font-smoothing: antialiased;
    cursor: pointer;
    position: absolute;
    z-index: 1;
    top: -2px;
    left: -2px;
    width: 44px;
    height: 44px;
    margin: 0;
    opacity: 0;
  }

  .custom-checkbox > .checkbox-label {
    font-size: inherit;
    font-family: inherit;
    line-height: inherit;
    display: inline-block;
    margin-bottom: 0;
    padding: 8px 15px 5px;
    cursor: pointer;
    touch-action: manipulation;
  }

  .custom-checkbox > label::before {
    content: "";
    box-sizing: border-box;
    position: absolute;
    top: 0;
    left: 0;
    width: 40px;
    height: 40px;
    border: 2px solid currentcolor;
    background: transparent;
  }

  .custom-checkbox > input[type="checkbox"]:focus + label::before {
    border-width: 4px;
    outline: 3px dashed #228bec;
  }

  .custom-checkbox > label::after {
    box-sizing: content-box;
    content: "";
    position: absolute;
    top: 11px;
    left: 9px;
    width: 18px;
    height: 7px;
    transform: rotate(-45deg);
    border: solid;
    border-width: 0 0 5px 5px;
    border-top-color: transparent;
    opacity: 0;
    background: transparent;
  }

  .custom-checkbox > input[type="checkbox"]:checked + label::after {
    opacity: 1;
  }

  .visually-hidden {
    position: absolute;
    width: 1px;
    height: 1px;
    margin: -1px;
    padding: 0;
    overflow: hidden;
    clip: rect(0, 0, 0, 0);
    border: 0;
  }

  .btn {
    border: 1px solid black;
    border-radius: 5px;
    padding: 5px 10px;
    background-color: white;
    color: black;
    font-family: Arial, sans-serif;
    font-weight: 400;
  }

  .btn-group {
    display: flex;
    flex-direction: row;
    gap: 10px;
  }

  .btn_danger {
    background-color: red;
    opacity: 0.7;
    color: white;
  }

  @media only screen and (min-width: 40rem) {
    label,
    input,
    .custom-checkbox {
      font-size: 19px;
      font-size: 1.9rem;
      line-height: 1.31579;
    }
  }
</style>
