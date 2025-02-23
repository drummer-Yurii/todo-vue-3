<script setup>
import { ref } from 'vue';

const newTodo = ref('');
const todosData = JSON.parse(localStorage.getItem('todos')) || [];
const todos = ref(todosData);

const addTodo = () => {
  if (newTodo.value) {
    todos.value.push({
      done: false,
      content: newTodo.value,
    });
    newTodo.value = '';
  }
};
const doneTodo = (todo) => {
  todo.done = !todo.done;
};
</script>

<template>
  <h1>Todo App</h1>
  <form @submit.prevent="addTodo">
    <label>New todo</label>
    <input type="text" v-model="newTodo" />
    <button type="submit">Add new todo</button>
  </form>
  <h2>Todo List</h2>
  {{ todos }}
  <ul>
    <li v-for="(todo, index) in todos" :key="index">
      <span :class="{ done: todo.done }" @click="doneTodo(todo)">
        {{ todo.content }}
      </span>
    </li>
  </ul>
</template>
