<script setup lang="ts">
defineProps({
  code: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  }
})
</script>
<template>
  <span v-html="code" :title="description" />
</template>
