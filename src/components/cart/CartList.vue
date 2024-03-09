<script setup>
import CartItem from "@/components/cart/CartItem.vue";
import {inject} from "vue";

defineProps({
  cart: Array
})
const {addToCart} = inject('useMainProvider');
</script>
<template>
  <div class="flex flex-col gap-5">
    <CartItem
        v-for="item of cart"
        :id="item.productId"
        :title="item.title"
        :price="Number(item.price)"
        :image-url="item.imageUrl"
        :remove-to-cart="() => addToCart(item)"
    />
  </div>
</template>