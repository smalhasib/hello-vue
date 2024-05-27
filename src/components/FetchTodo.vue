<script setup lang="ts">

import {ref, watch} from "vue";

let todoId = ref(1)
let todoData = ref(null)

async function fetchTodo(id: number) {
  todoData.value = null
  const res = await fetch(
      `https://jsonplaceholder.typicode.com/todos/${id}`
  )
  todoData.value = await res.json()
}
watch(todoId, (newTodoId) => {
  fetchTodo(newTodoId)
})

fetchTodo(todoId.value)
</script>

<template>
  <div class="p-10">
    <p class="p-2 text-xl">Todo id: {{ todoId }}</p>
    <button class="border-solid bg-gray-500 text-white px-4 py-2" @click="todoId++" :disabled="!todoData">Fetch Next Todo</button>
    <p class="mt-4" v-if="!todoData">Loading...</p>
    <pre class="mt-4" v-else>{{ todoData }}</pre>
  </div>
</template>
