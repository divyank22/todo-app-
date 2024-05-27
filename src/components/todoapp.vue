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
};
</script>

<template>
  <div class="todo-app">
    <div class="task-input">
      <h1 class="hed">title</h1>
      <input class="inputt" v-model="title" @keyup.enter="addtodo" placeholder="Add new title" />
      <h1 class="hed" >description</h1>
      <input class="inputd" v-model="description" @keyup.enter="addtodo" placeholder="Add new description" />
      <br />
      <button @click="addtodo">Add Todo</button>
  </div>
  <h2>Todos</h2>
  <ul>
    <li v-for="(todo, i) in todos" :key="i">
      Title:{{ todo.title }}
      <p>description:{{ todo.description }}</p>
      <button @click="removetask(i)">Remove</button>
    </li>
  </ul>
  </div>
</template>
<style scoped>
.task-input {
  margin: 9vh 27vw;
  width: 36vw;
  background-color: gainsboro;
}

li {
  list-style: none;
}

.inputt {
  width: 30vw;
  margin: 2vh 3vw;
  padding: 0.8%;
  border-radius: 12%;
  border: 0.3vw solid black;
}

.inputd {
  width: 30vw;
  height: 20vh;
  margin: 2vh 3vw;
  padding: 0.8%;
  border-radius: 12%;
  border: 0.3vw solid black;
}
.hed{
  margin: 0 0 0 1vw;
}
</style>
