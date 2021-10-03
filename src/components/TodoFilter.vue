<template>
  <div class="filter" @click="filtrar">
    <p class="filter__btn">All</p>
    <p class="filter__btn">Active</p>
    <p class="filter__btn">Completed</p>
  </div>
</template>

<script>
import { inject } from "@vue/runtime-core";
export default {
  setup() {
    const stateFilter = inject("stateFilter");

    const filtrar = (e) => {
      if (e.target.className === "filter__btn") {
        stateFilter.value = e.target.textContent;
        e.path[1].childNodes.forEach((element) => {
          element.classList.remove("filter__active")
        });
        e.target.classList.add("filter__active")
      }
    };

    return { filtrar };
  },
};
</script>

<style>
.filter {
  display: flex;
  align-items: center;
  justify-content: center;
  column-gap: 18px;
  cursor: pointer;
  font-size: 16.2px;
}
.filters-container .filter {
  background-color: var(--Very-Dark-Desaturated-Blue);
  list-style: none;
  padding: 1.2rem 1rem;
  margin-top: 1.4rem;
  border-radius: 6px;
}
.filter__btn {
  color: var(--Very-Dark-Grayish-Blue);
  transition: color 0.4s;
}
.filter__btn:hover {
  color: var(--Light-Grayish-Blue-hover);
}
.filter__active {
  color: var(--Bright-Blue);
}
</style>
