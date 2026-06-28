<script setup lang="ts">
  import {ref} from "vue";

  const emit = defineEmits<{
    submit: [payload: {type: string; query: string}]
  }>()

  const type = ref('ip')
  const query = ref('')
  const options = ["IP", "Domain", "ASN", "TLD"]

  function handleSubmit() {
    if(!query.value.trim()) {
      return
    }

    emit("submit", {type: type.value, query: query.value.trim()})
  }
</script>

<template>
  <div class="lookup-bar">
    <select v-model="type" class="lookup-select">
      <option v-for="opt in options" :key="opt" :value="opt.toLowerCase()">
        {{opt}}
      </option>
    </select>

    <input v-model="query" type="text" placeholder="Enter query" class="lookup-input" @keydown.enter="handleSubmit"/>

    <button :disabled="!query.trim()" class="lookup-button" @click="handleSubmit()">
      Submit
    </button>
  </div>
</template>

<style scoped>

</style>