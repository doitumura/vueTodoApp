<script setup>
import { ref, onMounted } from "vue";

let id = 0;
const newTodo = ref("");
const todos = ref([]);

const addTodo = () => {
  todos.value.push({ id: id++, text: newTodo.value, edit: false });
  newTodo.value = "";
};

const removeTodo = (todo) => {
  todos.value = todos.value.filter((t) => t !== todo);
};

const editTodo = (todo) => {
  todo.edit = true;
};

const updateTodo = (todo) => {
  todo.edit = false;
};

const writeToLocalstorage = () => {
  const todosJson = JSON.stringify(todos);
  localStorage.setItem("todos", todosJson);
  window.removeEventListener("beforeunload", writeToLocalstorage);
};

onMounted(() => {
  const localStorageTodos = JSON.parse(localStorage.getItem("todos"))._value;
  if (localStorageTodos) todos.value = localStorageTodos;

  window.addEventListener("beforeunload", writeToLocalstorage);
});
</script>

<template>
  <div>
    <h1 class="heading">タスク管理アプリ</h1>

    <div class="todo-input">
      <h2>タスクを追加する</h2>
      <form @submit.prevent="addTodo">
        <input v-model="newTodo" />
        <button>追加</button>
      </form>
    </div>

    <div class="todo-list">
      <h2 v-if="todos.length > 0" class="list-heading">タスク一覧</h2>
      <ul>
        <li v-for="todo in todos" :key="todo.id">
          <form v-if="todo.edit" @submit.prevent="updateTodo(todo)">
            <input v-model="todo.text" />
            <button>更新</button>
          </form>
          <div v-else>
            <span>{{ todo.text }}</span>
            <button @click="editTodo(todo)">編集</button>
            <button @click="removeTodo(todo)">削除</button>
          </div>
        </li>
      </ul>
    </div>
  </div>
</template>

<style scoped>
.heading {
  font-size: 70px;
}

.todo-input {
  margin-top: 20px;
}

form {
  display: flex;
  justify-content: left;
}

input {
  height: 20px;
}

button {
  height: 20px;
  line-height: 12px;
  font-size: 12px;
}

.todo-list {
  margin-top: 30px;
}

ul {
  padding-left: 15px;
}

span {
  margin-right: 5px;
  height: 20px;
}
</style>
