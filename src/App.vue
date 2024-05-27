<script setup lang="ts">
import FetchTodo from "@/components/FetchTodo.vue";
import ChildComp from "@/components/ChildComp.vue";
import Todos from "@/components/Todos.vue";
import Basics from "@/components/Basics.vue";
import {ref} from "vue";

const greeting = ref("Hello from parent")
const childMsg = ref("No child message yet")
</script>

<template>
  <Basics/>
  <Todos/>
  <FetchTodo/>
  <ChildComp :msg="greeting" @response="msg => childMsg = msg">
    This is some slot content!
  </ChildComp>
  <p class="ml-10 p-2 text-xl">{{ childMsg }}</p>
</template>