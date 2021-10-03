<template>
  <li class="todo-item">
    <div class="todo-item__container">
      <div
        @click="completed(todo.id)"
        class="circle-check"
        :class="todo.state ? 'check' : 'no-check'"
      >
        <img
          src="../assets/icon-check.svg"
          alt="icon check"
          class="check-svg"
        />
      </div>
      <p
        @click="completed(todo.id)"
        class="task"
        :class="
          todo.state
            ? 'task-completed'
            : 'task-incompleted'
        "
        >{{ todo.text }}</p
      >
    </div>
    <img
      @click="deleteTask(todo.id)"
      src="../assets/icon-cross.svg"
      alt="icon delete"
      class="todo-item__deleteTask"
    />
  </li>
</template>

<script>
import { inject } from "@vue/runtime-core";
export default {
  props: {
    todo: { type: Object, required: true },
  },
  setup() {
    const todos = inject("todos");

    const deleteTask = (id) => {
      todos.value = todos.value.filter((item) => item.id !== id);
    };
    const completed = (id) => {
      todos.value = todos.value.map((item) => {
        if (item.id == id) {
          item.state = !item.state;
        }
        return item;
      });
    };

    return { deleteTask, completed };
  },
};
</script>
<style>
.todo-item {
  display: flex;
  align-items: center;
  justify-content: space-between;
  background-color: var(--Very-Dark-Desaturated-Blue);
  list-style: none;
  padding: 1.3125rem 1.6875rem;
  border-bottom: 1px solid var(--Very-Dark-Grayish-Blue-border);
}
.todo-item__container {
  display: flex;
  align-items: center;
}
.circle-check {
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  padding: 9px 8px;
  margin-right: 1.51rem;
  cursor: pointer;
  background: transparent;
  border: 1px solid var(--Very-Dark-Grayish-Blue-border);
}
.circle-check__check-svg {
  height: 10px;
}
.check {
  background-image: var(--Check-Background);
}
.no-check {
  background-color: transparent;
  transition: border-color 0.4s;
}
.no-check:hover {
  border-color: #57ddff;
}
.no-check .check-svg {
  visibility: hidden;
}
.task::first-letter {
  text-transform: uppercase;
}
.task {
  cursor: pointer;
  padding-top: 4px;
}
.task-completed {
  text-decoration: line-through;
  color: var(--Very-Dark-Grayish-Blue);
}
.task-incompleted {
  color: var(--Light-Grayish-Blue);
  text-decoration: none;
}
.todo-item__deleteTask {
  cursor: pointer;
}
</style>
