<script setup>
import Card from './Card.vue'
</script>

<template>
  <div class="grid grid-cols-4 gap-5">
    <Card
        title="Кросовки крутые 1"
        :price="5000"
        img="/sneakers/sneakers-1.jpg"
    />
    <Card
        title="Кросовки крутые 2"
        :price="5000"
        img="/sneakers/sneakers-1.jpg"
    />
    <Card
        title="Кросовки крутые 3"
        :price="5000"
        img="/sneakers/sneakers-1.jpg"
    />
    <Card
        title="Кросовки крутые 4"
        :price="5000"
        img="/sneakers/sneakers-1.jpg"
    />
    <Card
        title="Кросовки крутые 5"
        :price="5000"
        img="/sneakers/sneakers-1.jpg"
    />
  </div>
</template>