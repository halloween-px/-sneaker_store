<script setup>
import Card from './Card.vue'

defineProps({
  products: Array
})

const emit = defineEmits(['addToFavorites', 'addToCart'])

</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
        v-for="item of products"
        :id="item.id"
        :key="item.id"
        :title="item.title"
        :price="Number(item.price)"
        :is-favorite="item.isFavorite"
        :is-added="item.isAdded"
        :addToFavorites="() => emit('addToFavorites', item)"
        :add-to-card="() => emit('addToCart', item)"
        :imageUrl="item.imageUrl"
    />
  </div>
</template>