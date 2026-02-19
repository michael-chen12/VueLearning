# Vue Lesson Four: Form Patterns and Component v-model

## What you learned

- Native `v-model` binds directly to input values.
- Component `v-model` uses `modelValue` prop + `update:modelValue` event.
- Keep validation in the parent when that state affects app logic.
- Use computed values for clean form rules (`canAdd`, `isDuplicate`, `normalizedInput`).

## Simple code examples

### 1) Native `v-model`

```vue
<input v-model="name" placeholder="Your name" />
```

### 2) Component `v-model`

```vue
<ModelTextInput v-model="hobbyInput" label="New hobby" />
```

### 3) Child component contract

```vue
<script setup lang="ts">
defineProps<{ modelValue: string }>()
const emit = defineEmits<{ (e: 'update:modelValue', value: string): void }>()
</script>
```

## Mini exercise

Build a small task manager using component `v-model`:

1. Create `TaskTextInput.vue` with `modelValue` and `update:modelValue`.
2. In `App.vue`, keep `taskInput` and `tasks` in parent state.
3. Add computed rules for trimming spaces, blocking empty tasks, and blocking duplicate tasks (case-insensitive).
4. Disable `Add Task` button when invalid.
5. Add Enter key support to submit.

## References

- Forms and native `v-model`: https://vuejs.org/guide/essentials/forms.html
- Component `v-model`: https://vuejs.org/guide/components/v-model.html
- Computed properties: https://vuejs.org/guide/essentials/computed.html
