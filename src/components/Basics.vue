<script setup lang="ts">
import { reactive, ref } from 'vue'

const message = ref('Hello Vue!')
const counter = reactive({ count: 0 })
const inputText = ref('')
const awesome = ref(true)

const titleClass = ref('title')


const increment = () => counter.count++
const onInput = (event: Event) => {
  inputText.value = (event.target as HTMLInputElement).value
}
const toggle = () => awesome.value = !awesome.value
</script>

<template>
  <div class="p-10">
    <!-- v-bind:class="titleClass" is the same as :class="titleClass -->
    <h1 :class="titleClass">{{ message.split('').reverse().join('') }}</h1>
    <!-- v-on:click="increment" is the same as @click="increment" -->
    <button @click="increment">Count is: {{ counter.count }}</button>
    <br>
    <!-- v-model="inputText" is the same as :value="inputText" @input="onInput" -->
    <input v-model="inputText" class="input" placeholder="Type here" />
    <p class="borderedText">{{ inputText }}</p>

    <br>
    <br>
    <br>

    <button @click="toggle"
      class="bg-green-500 text-white px-10 py-1 hover:bg-red-600 hover:duration-[543] rounded">Toggle</button>
    <h1 v-if="awesome" class="text-xl p-4 font-bold text-green-500">Vue is awesome!</h1>
    <h1 v-else class="text-xl p-4 font-bold text-red-500">Oh no 😢</h1>
  </div>
</template>

<style>
.title {
  color: red;
}

.input {
  padding: 10px;
  margin: 10px;
  font-size: medium;
}

.borderedText {
  border: 1px solid black;
  padding: 10px;
  margin: 10px;
  font-size: large;
  width: 11rem;
}
</style>