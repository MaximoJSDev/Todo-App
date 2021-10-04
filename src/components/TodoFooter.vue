<template>
  <li class="footer todo-item">
    <p>{{ countActives }} Items left</p>
    <TodoFilter />
    <p @click="deleteCompleted" class="footer__clear">Clear completed</p>
  </li>
  <div class="newFooter"></div>
</template>

<script>
import { computed, inject, onMounted } from "@vue/runtime-core";
import TodoFilter from "./TodoFilter.vue";

export default {
  components: { TodoFilter },
  setup() {
    const todos = inject("todos");

    const countActives = computed(() => {
      return todos.value.filter((item) => item.state === false).length;
    });
    const deleteCompleted = () => {
      todos.value = todos.value.filter((item) => item.state === false);
    };
    const CreateNewFooter = () => {
      const newFooter = document.querySelector(".newFooter");
      const filter = document.querySelector(".filter");
      newFooter.appendChild(filter);
      newFooter.classList.add("filters-container");

    };
    onMounted(() => {
      if (window.screen.width <= 600) {
        CreateNewFooter()
      }
    });
    return { countActives, deleteCompleted, CreateNewFooter };
  },
};
</script>

<style>
.footer {
  display: flex;
  align-items: center;
  justify-content: space-between;
  list-style: none;
  font-weight: 700;
  font-size: 15px;
  color: var(--Very-Dark-Grayish-Blue);
  border-end-end-radius: 6px;
  border-end-start-radius: 6px;
  border-bottom: none;
  padding: 1.3rem 1.2rem !important;
}
 p {
  margin: 0;
}
.footer__clear {
  cursor: pointer;
  transition: color 0.4s;
}
.footer__clear:hover {
  color: var(--Light-Grayish-Blue-hover);
}
</style>
