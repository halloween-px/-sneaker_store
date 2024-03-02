<script setup>
import Card from './Card.vue'

defineProps({
  products: Array
})

const emit = defineEmits(['addToFavorites'])

</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
        v-for="item of products"
        :id="item.id"
        :key="item.id"
        :title="item.title"
        :price="item.price"
        :is-favorite="item.isFavorite"
        :is-added="false"
        :addToFavorites="() => emit('addToFavorites', item)"
        :imageUrl="item.imageUrl"
    />
  </div>
</template>