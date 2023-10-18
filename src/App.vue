<script setup>
import { ref } from 'vue'

let id = 0
const todos = ref([])
const newTodo = ref('')

function addTodo() {
  if (!newTodo.value) return
  todos.value.push({
    id: id++,
    text: newTodo.value
  })
  newTodo.value = ''
}

function removeTodo(todo) {
  todos.value = todos.value.filter((t) => t !== todo)
}
</script>

<template>
  <h2 class="text-2xl mb-4 text-center">Todo List</h2>
  <form action @submit.prevent>
    <input
      type="text"
      class="p-2 border rounded w-full mb-4"
      placeholder="Add a new task..."
      id="newTodo"
      v-model="newTodo"
      @keyup.enter="addTodo"
    />
  </form>
  <ul id="taskList">
    <li
      class="flex justify-between items-center border p-2 mb-2"
      v-for="todo in todos"
      :key="todo.id"
    >
      {{ todo.text }}
      <button
        class="bg-red-500 hover:bg-red-600 text-white px-2 py-1 rounded"
        @click="removeTodo(todo)"
      >
        Remove
      </button>
    </li>
  </ul>
  <button class="mt-4 bg-blue-500 hover:bg-blue-600 text-white p-2 rounded w-full" @click="addTodo">
    Add
  </button>
</template>
