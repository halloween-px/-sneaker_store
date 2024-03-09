<script setup>
  import {inject} from "vue";

  const {toggleSidebar} = inject('useMainProvider');
</script>
<template>
  <header class="flex justify-between border-b border-slate-200 px-10 py-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-11" />
      <div>
        <h2 class="font-bold text-xl uppercase">Vue Sneakers</h2>
        <p class="text-slate-400">Магазин лучших кроссовок</p>
      </div>
    </div>

    <ul class="flex items-center gap-10">
      <li>
        <button
            type="button"
            class="flex items-center gap-3 cursor-pointer"
            @click="toggleSidebar">
          <img src="/cart.svg" alt="Cart" />
          <b>1205 руб.</b>
        </button>
      </li>
      <li>
        <button type="button" class="flex items-center gap-3 cursor-pointer">
          <img src="/heart.svg" alt="Favorite" />
          <span>Закладки</span>
        </button>
      </li>
      <li>
        <button type="button" class="flex items-center gap-3 cursor-pointer">
          <img src="/profile.svg" alt="Favorite" />
          <span>Профиль</span>
        </button>
      </li>
    </ul>
  </header>
</template>