<script setup>
import { ref, onMounted, onUnmounted } from "vue";
const title = ref("");
const description = ref("");
const todos = ref([]);
onMounted(() => {
  const storedTodos = JSON.parse(localStorage.getItem("todos") || "[]");
  todos.value = storedTodos;
});
const saveTodos = () => {
  localStorage.setItem("todos", JSON.stringify(todos.value));
};
const addtodo = () => {
  if (title.value.trim() !== "" && description.value.trim() !== "") {
    todos.value.push({ title: title.value, description: description.value });
    title.value = "";
    description.value = "";
    saveTodos();
  }
};
const removetask = (index) => {
  todos.value.splice(index, 1);
  saveTodos();
};
</script>
<template>
  <div class="todo-app">
    <div class="task-input">
      <h1 class="hea">title</h1>
      <input class="inputt" v-model="title" @keyup.enter="addtodo" placeholder="Add new title" />
      <h1 class="hea">description</h1>
      <input class="inputd" v-model="description" @keyup.enter="addtodo" placeholder="Add new description" />
      <br />
      <button @click="addtodo">Add Todo</button>
    </div>
  </div>
  <h2 class="head">Todos</h2>
  <div class="container">
  <ul class="card">
    <li v-if="todos.length > 0"  class="todol" v-for="(todo, i) in todos" :key="i">
      Title:{{ todo.title }}
      <p>description:{{ todo.description }}</p>
      <button @click="removetask(i)">Remove</button>
      <br>
    </li>
    <li v-else>
      <p>todo is empty</p>
    </li>
  </ul>
</div>

</template>

