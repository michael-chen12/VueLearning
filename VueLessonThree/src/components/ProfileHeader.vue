<script setup lang="ts">
defineProps<{
  name: string;
  age: number;
  ageLabel: string;
}>();
</script>

<template>
  <header>
    <h1>Hello, {{ name }}</h1>
    <p>Age: {{ age }}</p>
    <p>Status: {{ ageLabel }}</p>
  </header>
</template>
