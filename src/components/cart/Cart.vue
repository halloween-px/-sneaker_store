<script setup>
import CartItem from "@/components/cart/CartItem.vue";
import CartHeader from "@/components/cart/CartHeader.vue";
import CartFooter from "@/components/cart/CartFooter.vue";
import CartList from "@/components/cart/CartList.vue";
</script>

<template>
  <div class="fixed z-10 top-0 h-full w-full bg-black opacity-70"/>
  <div
      class="flex flex-col justify-between fixed h-full z-10 top-0 h-full right-0 w-96 bg-white px-10 py-7"
  >
    <CartHeader/>
    <div class="flex flex-col flex-1 justify-between">
      <CartList/>
      <div>
        <CartFooter />
      </div>
    </div>
  </div>
</template>
