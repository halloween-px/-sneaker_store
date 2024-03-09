<script setup>
import CartHeader from "@/components/cart/CartHeader.vue";
import CartFooter from "@/components/cart/CartFooter.vue";
import CartList from "@/components/cart/CartList.vue";
import {inject} from "vue";

const {sidebar, toggleSidebar, cart} = inject('useMainProvider');

</script>

<template>
  <transition name="animation-card">
    <div v-if="sidebar" class="fixed z-10 top-0 h-full w-full">
      <div class="fixed z-10 top-0 h-full w-full bg-black opacity-70 dark-block" @click="toggleSidebar"/>
      <div
          class="flex flex-col justify-between fixed h-full z-10 top-0 h-full right-0 w-96 bg-white px-10 py-7 slider-block"
      >
        <CartHeader/>
        <div class="flex flex-col flex-1 justify-between">
          <CartList :cart="cart"/>
          <div>
            <CartFooter/>
          </div>
        </div>
      </div>
    </div>
  </transition>
</template>

<style>
.animation-card-enter-active,
.animation-card-leave-active,
 .dark-block,
 .slider-block{
  transition: all .3s ease-in-out;
}

.animation-card-enter-from .slider-block, .animation-card-leave-to .slider-block{
  transform: translateX(100%);
}

.animation-card-enter-from .dark-block, .animation-card-leave-to .dark-block{
  opacity: 0;
}

</style>
