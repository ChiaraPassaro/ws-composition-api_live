<script setup lang="ts">
defineProps({
  data: {
    type: Array,
    required: true
  }
})
</script>

<template>
  <ul class="list list--inline">
    <li v-for="(datum, i) in data" :key="`list-element-${i}`" class="list-element">
      <slot name="element" :data="datum" :idx="i"></slot>
    </li>
  </ul>
</template>

<style lang="scss" scoped>
.list {
  margin: auto;
  padding: 1rem;
  list-style: none;
  &--inline {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
  }
  &-element {
    padding: 0.3rem;
  }
}
</style>
