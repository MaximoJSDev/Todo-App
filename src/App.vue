<template>
  <TodoApp />
</template>

<script>
import TodoApp from "./components/TodoApp.vue";

export default {
  name: "App",
  components: { TodoApp },
}
</script>

<style>
*,
*::after,
*::before {
  box-sizing: border-box;
}
html {
  --Mobile: 375px;
  --Desktop: 1440px;

  --Bright-Blue: hsl(220, 98%, 61%);
  --Check-Background: linear-gradient(
    to bottom right,
    hsl(192, 100%, 67%),
    hsl(280, 87%, 65%)
  );
  /* ### Dark Theme */
  --Very-Dark-Blue: rgb(22, 23, 34);
  --Very-Dark-Desaturated-Blue: rgb(37, 39, 60);
  --Light-Grayish-Blue: hsl(234, 39%, 85%);
  --Light-Grayish-Blue-hover: hsl(235, 32%, 92%);
  --Dark-Grayish-Blue: hsl(234, 11%, 52%);
  --Very-Dark-Grayish-Blue: hsl(233, 14%, 35%);
  --Very-Dark-Grayish-Blue-border: hsl(237, 14%, 26%);
}
html.light {
  --Very-Dark-Blue: hsl(236, 33%, 92%);
  --Very-Dark-Desaturated-Blue: hsl(0, 0%, 98%);
  --Light-Grayish-Blue: hsl(235, 19%, 35%);
  --Very-Dark-Grayish-Blue-border: hsl(233, 11%, 84%);
  --Very-Dark-Grayish-Blue: hsl(236, 9%, 61%);
}
body {
  font-family: "Josefin Sans", sans-serif;
  font-size: 20px;
  background: var(--Very-Dark-Blue);
}
</style>
