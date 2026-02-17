<script setup lang="ts">
type Hobby = { id: number; name: string };

defineProps<{ hobbies: Hobby[] }>();
const emit = defineEmits<{
  (e: "remove-hobby", id: number): void;
}>();
</script>

<template>
  <ul>
    <li v-for="hobby in hobbies" :key="hobby.id">
      {{ hobby.name }}
      <button @click="emit('remove-hobby', hobby.id)">Remove</button>
    </li>
  </ul>
</template>
