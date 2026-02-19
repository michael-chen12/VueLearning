<script setup lang="ts">
const props = defineProps<{
  modelValue: string;
}>();

const emit = defineEmits<{
  "update:modelValue": [value: string];
  "add-task": [];
}>();

function onInput(event: Event): void {
  const target = event.target as HTMLInputElement | null;
  emit("update:modelValue", target?.value ?? "");
}

function onAddtask(): void {
  emit("add-task");
}
</script>

<template>
  <input type="text" :value="props.modelValue" @input="onInput" />
  <button @click="onAddtask" :disabled="!props.modelValue.trim()">
    Add Task
  </button>
</template>

<style scoped></style>
