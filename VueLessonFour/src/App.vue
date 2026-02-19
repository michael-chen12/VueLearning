<template>
  <div>
    <h1>Task List</h1>
    <TaskTestInput v-model="taskInput" @add-task="addTask" />
    <p>Current Task: {{ taskInput }}</p>
    <ol>
      <li v-for="(task, index) in tasks" :key="`task-${index}`">
        {{ task }}
      </li>
    </ol>
  </div>
</template>

<script setup lang="ts">
import { ref, computed } from "vue";
import TaskTestInput from "./components/TaskTestInput.vue";
const taskInput = ref("");
const tasks = ref<string[]>([]);

const cleanTaskInput = computed(() => taskInput.value.trim());
const canAddTask = computed(() => cleanTaskInput.value.length > 0);
const isDuplicateTask = computed(() =>
  tasks.value.some(
    (task) => task.toLowerCase() === cleanTaskInput.value.toLowerCase(),
  ),
);

function addTask() {
  if (canAddTask.value && !isDuplicateTask.value) {
    tasks.value.push(cleanTaskInput.value);
    taskInput.value = "";
  }
}
</script>

<style scoped></style>
