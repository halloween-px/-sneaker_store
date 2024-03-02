<script setup>
import Header from "@/components/layouts/Header.vue";
import CartList from "@/components/product/CardList.vue";
import {onMounted, reactive, provide, ref, watch} from "vue";
import {getProducts, filtersProduct, getFavorites, deleteFavorite, postFavorites, searchKeyWord} from "@/data/products.vue";
import Select from "@/components/shared/Select.vue";
import Search from "@/components/shared/Search.vue";

const products = ref([]);
const filters = reactive({
  sort: '',
  filter: '',
});

const fetchFavorites = async () => {
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
  await fetchFavorites();
})

watch(filters, onSort);

provide('addToFavorites', addToFavorites)

</script>

<template>
  <div class="bg-white w-3/5 m-auto rounded-xl main-2 shadow-xl shadow-grey-200 mt-20">
    <Header />
    <div class="p-10">
      <div class="flex justify-between items-center mb-10">
        <h1 class="text-3xl font-bold">Все кроссовки</h1>
        <div class="flex items-center gap-4">
          <Select :onSelectChange="onSelectChange"/>
          <Search :on-search="onSearch" />
        </div>
      </div>
      <div class="mt-5">
        <CartList
            :products="products"
            @addToFavorites="addToFavorites"
        />
      </div>
    </div>
  </div>
</template>
