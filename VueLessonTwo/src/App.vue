<script setup lang="ts">
import { ref, computed } from 'vue'

type Hobby = { id: number; name: string }

const name = ref('Michael')
const age = ref(17)

const hobbyInput = ref('')
const hobbies = ref<Hobby[]>([])
let nextId = 1

const ageLabel = computed(() => (age.value >= 18 ? 'Adult' : 'Minor'))
const hobbyCount = computed(() => hobbies.value.length)

const normalizedInput = computed(() => hobbyInput.value.trim())
const isDuplicate = computed(() =>
  hobbies.value.some((h) => h.name.toLowerCase() === normalizedInput.value.toLowerCase()),
)
const canAddHobby = computed(() => normalizedInput.value.length > 0 && !isDuplicate.value)
const greeting = computed(() => `Good morning, ${name.value}!`)
function addHobby() {
  if (!canAddHobby.value) return
  hobbies.value.push({ id: nextId++, name: normalizedInput.value })
  hobbyInput.value = ''
}

function removeHobby(id: number) {
  hobbies.value = hobbies.value.filter((h) => h.id !== id)
}
</script>

<template>
  <input v-model="name" placeholder="Name" />
  <input v-model.number="age" type="number" min="0" />

  <p>Hello, {{ name }}</p>
  <p>Status: {{ ageLabel }}</p>
  <p>Total hobbies: {{ hobbyCount }}</p>

  <input v-model="hobbyInput" placeholder="Add hobby" />
  <button :disabled="!canAddHobby" @click="addHobby">Add</button>
  <p v-if="isDuplicate">Hobby already exists.</p>

  <ul>
    <li v-for="hobby in hobbies" :key="hobby.id">
      {{ hobby.name }}
      <button @click="removeHobby(hobby.id)">Remove</button>
    </li>
  </ul>

  <p>{{ greeting }}</p>
</template>
