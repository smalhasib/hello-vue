<script setup lang="ts">
import { reactive, ref } from 'vue'

const message = ref('Hello Vue!')
const counter = reactive({ count: 0 })
const inputText = ref('')

const titleClass = ref('title')
const inputClass = ref('input')
const borderedTextClass = ref('borderedText')


const increment = () => counter.count++
const onInput = (event: Event) => {
  inputText.value = (event.target as HTMLInputElement).value
}
</script>

<template>
  <!-- v-bind:class="titleClass" is the same as :class="titleClass -->
  <h1 :class="titleClass">{{ message.split('').reverse().join('') }}</h1>
  <!-- v-on:click="increment" is the same as @click="increment" -->
  <button @click="increment">Count is: {{ counter.count }}</button>
  <br>
  <!-- v-model="inputText" is the same as :value="inputText" @input="onInput" -->
  <input v-model="inputText" :class="inputClass" placeholder="Type here"/>
  <p :class="borderedTextClass">{{ inputText }}</p>
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