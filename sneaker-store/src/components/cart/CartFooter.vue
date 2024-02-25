<template>
  <div class="flex flex-col gap-5">
    <div class="flex items-end gap-2">
      <span>Итого:</span>
      <div class="flex-1 border-b border-dashed"/>
      <span class="font-bold">1000 руб.</span>
    </div>

    <div class="flex items-end gap-2">
      <span>Налог 5%:</span>
      <div class="flex-1 border-b border-dashed"/>
      <span class="font-bold">50 руб.</span>
    </div>
  </div>

  <button
      class="flex justify-center items-center gap-3 w-full py-3 mt-10 bg-lime-500 text-white rounded-xl transition active:bg-lime-700 hover:bg-lime-600"
  >
    Оформить заказ
    <img src="/arrow-next.svg" alt="Arrow"/>
  </button>
</template>