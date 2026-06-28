<script setup lang="ts">
defineProps<{
  data: Record<string, unknown> | null
  loading: boolean;
  error: string;
}>()
</script>

<template>
  <div v-if="loading" class="result-state">
    Loading...
  </div>

  <div v-else-if="error" class="result-state result-error">
    {{ error }}
  </div>

  <div v-else-if="data" class="result-box">
    <pre class="result-json">{{JSON.stringify(data, null, 2)}}</pre>
  </div>
</template>

<style scoped>

</style>