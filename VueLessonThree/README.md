# Vue Lesson Three: Components, Props, and Emits

## What you learned

- Break one big app into small components.
- Parent owns state.
- Child reads data with `props`.
- Child sends actions up with `emit`.
- Keep one-way data flow: parent -> child (data), child -> parent (events).

## Simple code examples

### 1) Parent passes props

```vue
<ProfileHeader :name="name" :age="age" />
```

### 2) Child defines props

```vue
<script setup lang="ts">
defineProps<{ name: string; age: number }>()
</script>
```

### 3) Child emits event

```vue
<script setup lang="ts">
const emit = defineEmits<{ (e: 'remove-hobby', id: number): void }>()
</script>

<template>
  <button @click="emit('remove-hobby', hobby.id)">Remove</button>
</template>
```

## Mini exercise

Build a `Task` version of this lesson:

1. Create `TaskInput.vue` and `TaskList.vue`.
2. Parent (`App.vue`) owns `tasks`.
3. `TaskInput` emits `add-task`.
4. `TaskList` emits `remove-task`.
5. Add duplicate check (case-insensitive).
6. Show total task count using a computed value.

## References

- Props: https://vuejs.org/guide/components/props.html
- Component events: https://vuejs.org/guide/components/events
- Component basics: https://vuejs.org/guide/essentials/component-basics.html
