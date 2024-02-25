<script setup>
import Header from "@/components/layouts/Header.vue";
import CartList from "@/components/product/CardList.vue";
import {onMounted, reactive, ref, watch} from "vue";
import {getProducts, sortProduct, filtersProduct, searchProduct, searchKeyWord} from "@/data/products.vue";
import Select from "@/components/shared/Select.vue";
import Search from "@/components/shared/Search.vue";

const products = ref([]);
const filters = reactive({
  sort: '',
  filter: '',
});

onMounted(async () => {
  products.value = await getProducts();
})
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

watch(filters, onSort)

</script>

<template>
  <div class="bg-white w-3/5 m-auto rounded-xl shadow-xl shadow-grey-200 mt-20">
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
        <CartList :products="products" />
      </div>
    </div>
  </div>
</template>
