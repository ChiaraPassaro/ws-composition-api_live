<script setup lang="ts">
import { computed } from 'vue'
import List from './List.vue'
const emit = defineEmits(['update:modelValue'])

const props = defineProps({
  data: {
    type: Array,
    required: true
  },
  id: {
    type: String,
    required: true
  },
  label: {
    type: String,
    required: true
  },
  placeholder: {
    type: String,
    required: true
  },
  modelValue: {
    type: String,
    required: true
  },
  inline: {
    type: Boolean
  }
})

const value = computed({
  get() {
    return props.modelValue
  },
  set(value) {
    emit('update:modelValue', value)
  }
})
</script>
<template>
  <div class="search-wrapper">
    <div class="search-box">
      <label class="sr-only" :for="`search-input-${id}`">{{ label }}</label>
      <input
        v-model="value"
        :id="`search-input-${id}`"
        :placeholder="placeholder"
        class="search-input"
        type="text"
      />
    </div>
    <List :data="data" :inline="inline">
      <template #element="{ data }">
        <slot name="elementList" :data="data" />
      </template>
    </List>
  </div>
</template>

<style scoped lang="scss">
.search-wrapper {
  padding: 0.3rem;
  margin-block-start: 0.5rem;
  border-radius: 0.4rem;
  background-color: white;
  color: black;
}
.list {
  block-size: 20rem;
  overflow-y: auto;
  font-size: 2.2rem;
}

.search-input {
  inline-size: 100%;
  margin-block-end: 0.5rem;
  line-height: 2rem;
  &::placeholder {
    font-style: italic;
  }
}
</style>
