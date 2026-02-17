<script setup lang="ts">
import { ref, computed } from "vue";
import ProfileHeader from "./components/ProfileHeader.vue";
import HobbyInput from "./components/HobbyInput.vue";
import HobbyList from "./components/HobbyList.vue";

type Hobby = { id: number; name: string };

const name = ref("Michael");
const age = ref(17);
const hobbies = ref<Hobby[]>([]);
let nextId = 1;

const ageLabel = computed(() => (age.value >= 18 ? "Adult" : "Minor"));

function addHobby(rawName: string) {
  const normalized = rawName.trim();
  if (!normalized) return;

  const isDuplicate = hobbies.value.some(
    (h) => h.name.toLowerCase() === normalized.toLowerCase(),
  );
  if (isDuplicate) return;

  hobbies.value.push({ id: nextId++, name: normalized });
}

function removeHobby(id: number) {
  hobbies.value = hobbies.value.filter((h) => h.id !== id);
}
</script>

<template>
  <main>
    <ProfileHeader :name="name" :age="age" :age-label="ageLabel" />
    <HobbyInput :hobbies="hobbies" @add-hobby="addHobby" />
    <HobbyList :hobbies="hobbies" @remove-hobby="removeHobby" />
  </main>
</template>
