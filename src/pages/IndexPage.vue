<template>
  <div class="todo">
    <h1>To-Do List</h1>
    <div class="container q-mb-lg">
      <q-input
        class="todo-input"
        label="Add a new to-do item"
        v-model="newTodo"
      ></q-input>
      <q-btn color="primary" label="Add" @click="addTodo"></q-btn>
    </div>

    <ul>
      <li v-for="(todo, index) in state.todos" :key="index" class="q-mb-md">
        <q-checkbox v-model="todo.done"></q-checkbox>
        <span :class="{ done: todo.done }" class="q-mr-md">{{
          todo.text
        }}</span>
        <q-btn
          color="red"
          label="Remove"
          @click="removeTodo(index)"
          class="q-md"
        ></q-btn>
      </li>
    </ul>
  </div>
</template>

<script lang="ts" setup>
import { reactive, ref } from "vue";

const state = reactive({
  todos: [],
});
const newTodo = ref("");

function addTodo() {
  if (newTodo.value.trim() !== "") {
    state.todos.push({
      text: newTodo.value,
      done: false,
    });
    newTodo.value = "";
  }
}

function removeTodo(index) {
  state.todos.splice(index, 1);
}
</script>

<style>
.todo {
  display: flex;
  flex-direction: column;
  align-items: center;
}
.container {
  display: flex;
}
.todo-input {
  width: 200px;
  margin-right: 20px;
}
.done {
  text-decoration: line-through;
}
</style>
