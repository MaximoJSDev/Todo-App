<template>
  <header class="header">
    <div class="header__title-content">
      <h1 class="header__title">TODO</h1>
      <img
        :src="light"
        alt="icono noche/luna"
        @click="toggleLight"
        class="sun-night"
      />
    </div>
  </header>
  <main class="main">
    <TodoAppCreate />
    <TodoAppList />
    <span class="dragAndDrop">Drag and drop to reorder list</span>
  </main>
</template>

<script>
import { provide, ref, watchEffect } from "vue";
import TodoAppCreate from "./TodoAppCreate.vue";
import TodoAppList from "./TodoAppList.vue";

export default {
  components: { TodoAppCreate, TodoAppList },
  data() {
    return { light: require("@/assets/icon-sun.svg") };
  },
  methods: {
    toggleLight() {
      const html = document.documentElement;
      html.classList.toggle("light");
      if (html.classList.contains("light"))
        this.light = require("@/assets/icon-moon.svg");
      else this.light = require("@/assets/icon-sun.svg");
    },
  },
  setup() {
    const todos = ref([]);
    provide("todos", todos);

    if (localStorage.getItem("todos"))
      todos.value = JSON.parse(localStorage.getItem("todos"));
    watchEffect(() =>
      localStorage.setItem("todos", JSON.stringify(todos.value))
    );
  },
};
</script>

<style>
.header {
  display: flex;
  align-items: center;
  justify-content: center;
  background: no-repeat url("../assets/bg-desktop-dark.jpg") center/cover;
  min-height: 38vh;
}
.light .header {
  background-image: url("../assets/bg-desktop-light.jpg");
}
.header__title-content {
  width: 650px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  transform: translateY(-60px);
}
.header__title {
  color: #fff;
  font-size: 3.2rem;
  margin: 0;
  padding-top: 10px;
  letter-spacing: 20px;
}
.sun-night {
  height: 2.7rem;
  cursor: pointer;
  padding: 5px;
}
.main {
  width: 40.625rem;
  display: flex;
  align-items: center;
  justify-content: center;
  flex-direction: column;
  margin: auto;
  color: var(--Light-Grayish-Blue);
  transform: translateY(-155px);
}
.dragAndDrop {
  font-size: 14px;
  font-weight: bold;
  color: var(--Very-Dark-Grayish-Blue);
  margin-top: 2rem;
}
@media (max-width: 700px) {
  body {
    font-size: 18px !important;
  }
  .header {
    min-height: 265px;
    background-image: url("../assets/bg-mobile-dark.jpg");
  }
  .light .header {
    background-image: url("../assets/bg-mobile-light.jpg");
  }
  .header__title-content,
  .form,
  .todo-list {
    width: 88%;
  }
  .header__title-content {
    transform: translateY(-64px);
  }
  .header__title {
    font-size: 2.4rem;
  }
  .form {
    padding: 1.15rem 1rem;
  }
  .form__createTask {
    font-size: 17.4px;
  }
  .main {
    width: auto;
    transform: translateY(-135px);
  }
  .todo-item {
    padding: 0.9rem 1rem;
  }
  .circle-check {
    margin-right: 0.9rem;
  }
  .task {
    font-size: 16px;
  }
  .footer {
    font-size: 13px;
  }
  .filter {
    font-size: 16px;
    font-weight: bold;
  }
}
</style>
