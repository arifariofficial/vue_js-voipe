<template>
  <form @submit.prevent="onSubmit">
    <h2 class="label-wrapper">
      <label for="new-todo-input" class="label_lg">Mitä tänään pitäisi tehdä? </label>
    </h2>
    <input
      type="text"
      name="new-todo"
      id="new-todo-input"
      autocomplete="off"
      v-model.lazy.trim="label"
      class="input_lg"
    />
    <button type="submit" class="btn btn_primary btn_lg">Lisää</button>
  </form>
</template>

<script>
  export default {
    methods: {
      onSubmit() {
        if (this.label === "") {
          return;
        }
        this.$emit("todo-added", this.label);
        this.label = "";
      },
    },
    data() {
      return {
        label: "",
      };
    },
  };
</script>

<style scoped>
  .btn {
    margin-left: 10px;
    border: 1px solid black;
    border-radius: 5px;
    padding: 10px;
    background-color: white;
    color: black;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
    outline: none;
    transition: all 0.2s ease-in-out;
  }
</style>
