<script setup lang="ts">
import LookupBar from "./components/LookupBar.vue";
import ResultBox from "./components/ResultBox.vue";
import {ref} from "vue";

const result = ref<Record<string, unknown> | null>(null)
const loading = ref(false)
const error = ref('')

async function handleSubmit(payload: {type: string, query: string}) {
  loading.value = true
  error.value = ''
  result.value = null

  try {
    const res = await fetch(`https://ipapi.nilsb.tech/v1/${payload.type.toLowerCase()}/${encodeURIComponent(payload.query)}`)
    console.log(res)

    if(!res.ok) {
      throw new Error(`HTTP ${res.status}`)
    }

    result.value = await res.json()
  } catch(e) {
    error.value = e instanceof Error ? e.message : "Unknown error"
  } finally {
    loading.value = false
  }
}
</script>

<template>
  <div class="app-wrapper">
    <div class="glass-card app-card">
      <LookupBar @submit="handleSubmit" />
      <ResultBox :data="result" :loading="loading" :error="error" />
    </div>
  </div>
</template>
