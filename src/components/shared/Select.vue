<script setup>
defineProps({
  onSelectChange: Function
})
</script>

<template>
  <select
      @change="onSelectChange"
      class="py-2 px-3 border border-gray-200 focus:border-gray-400 rounded-md focus:outline-none"
  >
    <option value="name">По названию</option>
    <option value="price">По цене (дешевые)</option>
    <option value="-price">По цене (дорогие)</option>
  </select>
</template>