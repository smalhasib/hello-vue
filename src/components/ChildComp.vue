<script setup lang="ts">
const props = defineProps<{
  msg: string
}>()
const emit = defineEmits(["response"])

emit("response", "Hello from child component")
</script>

<template>
  <div class="p-10">
      <h2 class="text-3xl font-bold">{{ msg || 'No props passed yet' }}</h2>
  </div>
  <p class="m-4 text-3xl">
    <slot>Fallback Content</slot>
  </p>
</template>
