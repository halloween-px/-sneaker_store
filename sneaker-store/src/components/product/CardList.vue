<script setup>
import Card from './Card.vue'

defineProps({
  products: Array
})

</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
        v-for="item of products"
        :key="item.id"
        :title="item.title"
        :price="item.price"
        :is-favorite="true"
        :is-added="true"
        :imageUrl="item.imageUrl"
    />
  </div>
</template>