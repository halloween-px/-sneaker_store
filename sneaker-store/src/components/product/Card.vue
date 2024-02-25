<script setup>
defineProps({
  title: String,
  imageUrl: String,
  price: String,
  isAdded: Boolean,
  isFavorite: Boolean
})
</script>

<template>
  <div
      class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl"
  >
    <img
        :src="isFavorite ? '/like-2.svg' : '/like-1.svg'"
        alt="Like 1"
        class="absolute top-8 left-8"
    />

    <img :src="imageUrl" alt="Sneaker" />

    <p class="mt-2 title" v-html="title" />

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Цена:</span>
        <b>{{ price }} руб.</b>
      </div>

      <img
          :src="isAdded ? '/checked.svg' : '/plus.svg'"
          alt="Plus"
      />
    </div>
  </div>
</template>

<style>
  .title .search-text{
    color: red;
  }
</style>