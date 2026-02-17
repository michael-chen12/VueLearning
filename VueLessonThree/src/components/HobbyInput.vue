<script setup lang="ts">
import { ref, computed } from "vue";

type Hobby = { id: number; name: string };

const props = defineProps<{ hobbies: Hobby[] }>();
const emit = defineEmits<{
  (e: "add-hobby", value: string): void;
}>();

const input = ref("");

const normalized = computed(() => input.value.trim());
const isDuplicate = computed(() =>
  props.hobbies.some(
    (h) => h.name.toLowerCase() === normalized.value.toLowerCase(),
  ),
);
const canAdd = computed(
  () => normalized.value.length > 0 && !isDuplicate.value,
);

function submit() {
  if (!canAdd.value) return;
  emit("add-hobby", normalized.value);
  input.value = "";
}
</script>

<template>
  <section>
    <input v-model="input" placeholder="Add hobby" @keyup.enter="submit" />
    <button :disabled="!canAdd" @click="submit">Add</button>
    <p v-if="isDuplicate">Hobby already exists.</p>
  </section>
</template>
