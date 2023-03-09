<script setup>
import { ref } from "vue";

let id = 0

const newTodo = ref("");
const todos = ref([]);

const addTodo = () => {
  todos.value.push({id: id++, text: newTodo.value, edit: false})
  newTodo.value = ''
}

const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo)
}

const editTodo = (todo) => {
  todo.edit = true;
}

const updateTodo = (todo) => {
  console.log(todo)
  todo.edit = false
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
      <form v-if="todo.edit" @submit.prevent="updateTodo(todo)">
        <input v-model="todo.text">
        <button>更新</button>
      </form>
      <div v-else>
        <span>{{todo.text}}</span>
        <button @click="editTodo(todo)">編集</button>
        <button @click="removeTodo(todo)">削除</button>
      </div>
    </li>
  </ul>
</div>
</template>

<style scoped>
</style>
