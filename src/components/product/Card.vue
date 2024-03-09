<script setup>

defineProps({
  id: Number,
  title: String,
  imageUrl: String,
  price: Number,
  isAdded: Boolean,
  isFavorite: Boolean,
  addToFavorites: Function,
  addToCard: Function,
})

</script>

<template>

  <div
      class="relative bg-white border border-slate-100 rounded-3xl p-8 cursor-pointer transition hover:-translate-y-2 hover:shadow-xl"
  >
    <button type="button"
            class="absolute top-8 left-8"
            @click="addToFavorites"
    >
      <img
          :src="isFavorite ? '/-sneaker_store/like-2.svg' : '/-sneaker_store/like-1.svg'"
          alt="Like 1"
      />
    </button>

    <img :src="imageUrl" alt="Sneaker" />

    <p class="mt-2 title" v-html="title" />

    <div class="flex justify-between mt-5">
      <div class="flex flex-col">
        <span class="text-slate-400">Цена:</span>
        <b>{{ price }} руб.</b>
      </div>

      <button type="button" @click="addToCard">
        <img
            :src="isAdded ? '/-sneaker_store/checked.svg' : '/-sneaker_store/plus.svg'"
            alt="Plus"
        />
      </button>
    </div>
  </div>
</template>

<style>
  .title .search-text{
    color: red;
  }
</style>