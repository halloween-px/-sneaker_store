<script setup>
import CardList from "@/components/product/CardList.vue";
import {inject, onMounted, reactive, ref, watch} from "vue";
import {getProducts, filtersProduct, getFavorites, deleteFavorite, postFavorites, searchKeyWord} from "@/data/products.vue";
import Select from "@/components/shared/Select.vue";
import Search from "@/components/shared/Search.vue";

const products = ref([]);
const {cart, addToCart} = inject('useMainProvider');

const filters = reactive({
  sort: '',
  filter: '',
});

const newProducts = async () => {
  const favorites = await getFavorites();
  products.value = products.value?.map((product) => {
    const favorite = favorites.find(favorite => favorite.productId === product.id);
    if(!favorite) return product;
    return {
      ...product,
      isFavorite: true,
      favoriteId: favorite.id
    }
  })

  products.value = products.value?.map((product) => {
    const elementCart = cart.value.find(cart => cart.productId === product.id);
    if(!elementCart) return product;
    return {
      ...product,
      isAdded: true,
      cartId: elementCart.id
    }
  })
}
const fetchProducts = async () => {
  products.value = await getProducts();
}

const addToFavorites = async (product) => {
  if(!product.isFavorite) {
    product.isFavorite = true;
    const favorite = await postFavorites({productId: product.id});
    product.favoriteId = favorite.id;
  } else {
    product.isFavorite = false;
    await deleteFavorite(product.favoriteId);
  }
}
const onSelectChange = (event) => {
  filters.sort = event.target.value;
}
const onSearch = (e) => {
  filters.filter = e.target.value;
}
const onSort = async () => {
  products.value = await filtersProduct(filters.filter, filters.sort);
  searchKeyWord(products, filters.filter)
}

onMounted(async () => {
  await fetchProducts();
  await newProducts();
})

watch(filters, onSort);
</script>

<template>
  <div class="flex justify-between items-center mb-10">
    <h1 class="text-3xl font-bold">Все кроссовки</h1>
    <div class="flex items-center gap-4">
      <Select :onSelectChange="onSelectChange"/>
      <Search :on-search="onSearch" />
    </div>
  </div>
  <div class="mt-5">
    <CardList
        :products="products"
        @add-to-favorites="addToFavorites"
        @add-to-cart="addToCart"
    />
  </div>
</template>
