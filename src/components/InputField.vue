<script setup lang="ts">
import { useField } from 'vee-validate'

const props = defineProps<{ name: string; label: string }>()
defineOptions({
  inheritAttrs: false
})

const { value, errorMessage } = useField(() => props.name)
</script>
<template>
  <div style="display: flex; flex-direction: row;">
    <label :for="name">{{ label }}</label>
    <div style="display: flex; flex-direction: column; gap: 0.2rem">
      <input v-bind="$attrs" v-model="value" :name="name" />
      <span>{{ errorMessage }}</span>
    </div>
  </div>
</template>
