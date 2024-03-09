<script setup>
import {onMounted, provide, ref} from "vue";
import {getCart, postCart, deleteCart} from "@/data/products.vue";

const actionSidebar = () => {
  const sidebar = ref(false);
  const toggleSidebar = () => {
    sidebar.value = !sidebar.value;
  }

  return {
    sidebar, toggleSidebar,
  }
}

const actionCart = () => {
  const cart = ref([]);
  const removeToCart = async (cartProduct) => {
    cartProduct.isAdded = false;
    const prd = cart.value.find(cart => cart.id === cartProduct.id);
    if(prd) {
      cart.value.splice(cart.value.indexOf(prd), 1);
    }
    await deleteCart(cartProduct.id);
  }
  const addToCart = async (product) => {
    console.log(product)
    if(!product.isAdded) {
      product.isAdded = true;
      const productId = product.id;
      delete product.id;
      const productCart = await postCart({...product, productId});
      cart.value.push(productCart);
      product.cartId = productCart.id;
    } else {
      product.isAdded = false;
      const prd = cart.value.find(cart => cart.id === product.cartId);
      if(prd) {
        cart.value.splice(cart.value.indexOf(prd), 1);
      }
      await deleteCart(product.cartId);
    }
  }

  const cartPrice = () => {
    return cart.value.reduce((acc, product) => {
      acc += Number(product.price);
      return acc;
    }, 0)
  }

  onMounted(async () => {
    cart.value = await getCart();
    console.log(cart.value);
  })

  return {
    cart,
    addToCart,
    removeToCart,
    cartPrice,
  }
}

provide('useMainProvider', {
  ...actionSidebar(),
  ...actionCart(),
})
</script>

<template>
  <slot></slot>
</template>