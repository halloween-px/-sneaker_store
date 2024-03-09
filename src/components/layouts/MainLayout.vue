<script setup>

import Header from "@/components/layouts/Header.vue";
import Cart from "@/components/cart/Cart.vue";
import Home from "@/components/Home.vue";

</script>

<template>
  <div class="bg-white w-3/5 m-auto rounded-xl main-2 shadow-xl shadow-grey-200 mt-20">
    <Header />
    <div class="p-10">
      <Home/>
    </div>
  </div>
  <Cart />
</template>