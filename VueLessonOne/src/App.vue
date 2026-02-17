<script setup lang="ts">
import { reactive, ref } from 'vue'
interface State {
  name: string
  age: number
  isStudent: boolean
}
const state = reactive<State>({
  name: 'Michael',
  age: 17,
  isStudent: false,
})
const isShow = ref<boolean>(true)
const hobbies = reactive<string[]>(['Reading', 'Traveling', 'Cooking'])
</script>

<template>
  <div>
    <h1>Welcome, {{ state.name }}!</h1>
    <p v-show="isShow">Age: {{ state.age }}</p>
    <p v-show="isShow">Status: {{ state.isStudent ? 'Student' : 'Not a Student' }}</p>
  </div>
  <div>
    <button @click="state.age++">Increase Age</button>
    <button @click="state.isStudent = !state.isStudent">Toggle Student Status</button>
    <button @click="isShow = !isShow">{{ isShow ? 'Hide' : 'Show' }}</button>
  </div>
  <ol>
    <li v-for="hobby in hobbies" :key="hobby">{{ hobby }}</li>
  </ol>
  <section v-if="state.age >= 18">
    <h2>Adult Content</h2>
    <p>This content is only visible to users who are 18 years or older.</p>
  </section>
</template>
