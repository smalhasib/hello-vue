<script setup lang="ts">
import {computed, onMounted, ref} from 'vue'

let id = 0

interface Todo {
  id: number
  text: string
  done: boolean
}

const newTodo = ref('')
const hideCompleted = ref(false)
const todos = ref<Todo[]>([
  {id: id++, text: 'Learn Vue 3', done: true},
  {id: id++, text: 'Learn React', done: true},
  {id: id++, text: 'Build something awesome', done: false}
])
const filteredTodos = computed<Todo[]>(() => {
  return hideCompleted.value ? todos.value.filter((todo: Todo) => !todo.done) : todos.value
})

const pElementRef = ref<HTMLElement | null>(null)

onMounted(() => {
  (pElementRef.value as HTMLElement).textContent += " passed"
})

const addTodo = () => {
  if (newTodo.value.trim() === '') return
  todos.value.push({id: id++, text: newTodo.value, done: false})
  newTodo.value = ''
}

const removeTodo = (id: number) => {
  const index = todos.value.findIndex(todo => todo.id === id)
  todos.value.splice(index, 1)
}
</script>

<template>
  <div class="p-10">
    <p class="text-3xl">Todos</p>
    <br>
    <form @submit.prevent="addTodo">
      <input v-model="newTodo" class="border-solid border-2 border-green-500 px-4 py-2" required
             placeholder="Add new todo">
      <button class="bg-green-500 text-white border-solid rounded px-4 py-1 ml-4">Add Todo</button>
    </form>
    <br>
    <ul class="list-decimal">
      <li class="py-1" v-for="todo in filteredTodos" :key="todo.id">
        <input class="m-1" type="checkbox" v-model="todo.done">
        <span :class="{ ['line-through']:todo.done }">{{ todo.text }}</span>
        <button
            class="bg-gray-500 px-2 py-1 rounded hover:border-2 m-1 hover:border-solid hover:bg-white hover:text-black hover:border-black"
            @click="removeTodo(todo.id)">X
        </button>
      </li>
    </ul>
    <button
        class="mt-8 border-solid border-2 border-green-500 px-4 py-2 rounded-2xl hover:border-none hover:bg-green-500 hover:text-white"
        @click="hideCompleted = !hideCompleted">
      {{ hideCompleted ? 'Show all' : 'Hide completed' }}
    </button>
    <p ref="pElementRef" class="p-4 text-2xl">On Mounted Test</p>
  </div>
</template>
