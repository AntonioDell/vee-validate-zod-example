<script setup lang="ts">
import { toTypedSchema } from '@vee-validate/zod'
import { useForm } from 'vee-validate'
import { watch } from 'vue'
import { number, object, string } from 'zod'
import FieldArrayComponent from './components/FieldArrayComponent.vue'
import InputField from './components/InputField.vue'
import {promiseTimeout} from "@vueuse/core"

const props = defineProps<{ test?: string }>()

const validationSchema = toTypedSchema(
  object({
    name: string().min(1),
    rows: number().array()
  })
)

const { resetForm, validate, meta } = useForm({
  validationSchema
})

async function reset() {
  await promiseTimeout(500)
  resetForm({ values: { name: 'Hello World', rows: [1, 2, 3, 4] } })
}

watch(
  () => props.test,
  () => {
    reset()
  },
  { immediate: true }
)
</script>

<template>
  <main>
    <form @submit.prevent>
      <InputField label="Name" name="name"></InputField>
      <FieldArrayComponent />
    </form>

    {{ meta }}

    <button @click="reset">Reset</button>
    <button @click="validate">Validate</button>
  </main>
</template>

<style scoped></style>
