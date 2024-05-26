<script setup>
import { ref } from 'vue'
const title = ref('')
const description = ref('')
const todos = ref([]) // Initialize todos as an empty array
const addtodo = () => {
  if (title.value.trim() !== '' && description.value.trim() !== '') {
    todos.value.push({ title: title.value, description: description.value })
    title.value = ''
    description.value = ''
  }
}
const removetask = (index) => {
  todos.value.splice(index, 1)
}
</script>

<template>
  <div class="todo-app">
    <div class="task-input">
      <input v-model="title" @keyup.enter="addtodo" placeholder="Add new task" />
      <input v-model="description" @keyup.enter="addtodo" placeholder="Add new description" />
      <button @click="addtodo">Add Todo</button>
    </div>
    <ul>
      <li v-for="(todo, i) in todos" :key="i">
        {{ todo.title }}
        <p>{{ todo.description }}</p>
        <button @click="removetask(i)">Remove</button>
      </li>
    </ul>
  </div>
</template>