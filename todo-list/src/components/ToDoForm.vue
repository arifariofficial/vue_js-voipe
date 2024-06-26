<template>
  <form @submit.prevent="onSubmit">
    <label for="new-todo-input">Mitä tänään pitäisi tehdä? </label>
    <input
      type="text"
      name="new-todo"
      id="new-todo-input"
      autocomplete="off"
      v-model.lazy.trim="label"
    />
    <button type="submit">Lisää</button>
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
