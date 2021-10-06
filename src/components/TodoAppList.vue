<template>
  <ul class="todo-list">
    <draggable :list="todos">
      <transition-group>
        <TodoListItem v-for="todo in todos" :key="todo.id" :todo="todo" />
      </transition-group>
    </draggable>

    <li v-if="todos.length === 0" class="todo-item zero-todos">
      Create a new todo!
    </li>
    <TodoListFooter />
  </ul>
</template>

<script>
import { computed, inject, provide, ref } from "@vue/runtime-core";
import TodoListItem from "./TodoListItem.vue";
import TodoListFooter from "./TodoListFooter.vue";
import { VueDraggableNext } from "vue-draggable-next";

export default {
  components: { TodoListItem, TodoListFooter, draggable: VueDraggableNext },
  setup() {
    const todosTodos = inject("todos");
    const stateFilter = ref("All");
    const todos = computed(() => {
      if (stateFilter.value == "All") {
        return todosTodos.value;
      } else if (stateFilter.value == "Active") {
        return todosTodos.value.filter((item) => item.state === false);
      } else if (stateFilter.value == "Completed") {
        return todosTodos.value.filter((item) => item.state === true);
      }
    });
    provide("stateFilter", stateFilter);

    return { todos };
  },
};
</script>

<style>
.todo-list {
  width: 100%;
  padding: 0;
  border-radius: 6px;
  overflow: hidden;
  margin-top: 27px;
  box-shadow: 0px 48px 70px -10px rgba(0, 0, 0, 0.24);
}
.light .todo-list {
  box-shadow: 0px 30px 45px -10px rgba(0, 0, 0, 0.11);
}
.zero-todos.zero-todos {
  padding: 1.4rem 1.2rem;
}
</style>
