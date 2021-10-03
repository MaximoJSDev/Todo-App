<template>
  <form @submit.prevent="todoAdd" class="form">
    <div class="circle-check">
      <img src="../assets/icon-check.svg" alt="icon check" class="check" />
    </div>
    <input
      maxlength="44"
      required
      type="text"
      class="form__createTask"
      placeholder="Create a new todo..."
      v-model.trim="input"
    />
  </form>
</template>

<script>
import { inject, ref } from "@vue/runtime-core";

export default {
  setup() {
    const todos = inject("todos");
    const input = ref("");

    const todoAdd = () => {
      if (input.value === "") {
        console.log("vacio");
        return;
      }
      const todo = {
        text: input.value,
        state: false,
        id: Date.now(),
      };
      todos.value.push(todo);
      input.value = "";
    };

    return { todoAdd, input };
  },
};
</script>

<style>
.form {
  display: flex;
  align-items: center;
  justify-content: center;
  width: 100%;
  background-color: var(--Very-Dark-Desaturated-Blue);
  padding: 1.4375rem 1.6875rem;
  border-radius: 6px;
  box-shadow: 0px 21px 67px -7px rgba(0, 0, 0, 0.23);
}
.form__createTask {
  width: 100%;
  border: none;
  outline: none;
  background-color: transparent;
  color: var(--Light-Grayish-Blue);
  caret-color: var(--Bright-Blue);
  padding-top: 4px;
}
.form__createTask::placeholder {
  color: var(--Dark-Grayish-Blue);
}
.form .circle-check {
  cursor: default;
}
.form .check {
  visibility: hidden;
}
</style>
