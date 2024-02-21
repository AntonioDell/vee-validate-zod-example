<script setup lang="ts">
import { useFieldArray } from 'vee-validate'
import InputField from './InputField.vue'
const { fields, push, remove } = useFieldArray('rows')

function addRow() {
  push(null)
}
</script>
<template>
  <div
    v-for="(field, index) of fields"
    :key="field.key"
    style="display: flex; flex-direction: row; gap: 1rem"
  >
    <InputField :label="`Row ${index}:`" :name="`rows[${index}]`" type="number" />
    <button @click="remove(index)">Remove</button>
  </div>
  <button @click="addRow">Add row</button>
</template>
