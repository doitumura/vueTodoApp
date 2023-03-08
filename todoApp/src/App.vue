<script setup>
import { ref } from "vue";

let id = 0

const newTodo = ref("");
const todos = ref([]);

const addTodo = () => {
  todos.value.push({id: id++, text: newTodo.value})
  newTodo.value = ''
}

const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
<div>
  <form @submit.prevent="addTodo">
    <input v-model="newTodo">
    <button>Add Todo</button>
  </form>

  <ul>
    <li v-for="todo in todos" :key="todo.id">
      <span>{{todo.text}}</span>
      <button @click="removeTodo(todo)">削除</button>
    </li>
  </ul>
</div>
</template>

<style scoped>
</style>
