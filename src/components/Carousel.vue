<script setup>
import { ref, onMounted, onBeforeUnmount, nextTick } from "vue";

const items = ref([
  "https://images.unsplash.com/photo-1636484807469-e33af13716b7?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1yZWxhdGVkfDF8fHxlbnwwfHx8fHw%3D&auto=format&fit=crop&w=1650&q=80",
  "https://images.unsplash.com/photo-1616423841125-8307665a0469?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1yZWxhdGVkfDE1fHx8ZW58MHx8fHx8&auto=format&fit=crop&w=1650&q=80",
  "https://images.unsplash.com/photo-1566323526101-051f07ee8925?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1yZWxhdGVkfDEzfHx8ZW58MHx8fHx8&auto=format&fit=crop&w=1650&q=80",
  "https://images.unsplash.com/photo-1614082242765-7c98ca0f3df3?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1650&q=80",
  "https://images.unsplash.com/photo-1645447556627-137df9819feb?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1yZWxhdGVkfDV8fHxlbnwwfHx8fHw%3D&auto=format&fit=crop&w=1650&q=80",
]);

let carousel = null;
const newItem = ref("");
function addNewItem() {
  items.value.push(newItem.value);
  carousel.destroy();
  nextTick(() => {
    carousel = new Flickity("#carousel", {
      autoPlay: 1500,
      freeScroll: true,
      wrapAround: true,
    });
  });
}
onMounted(() => {
  carousel = new Flickity("#carousel", {
    freeScroll: true,
    wrapAround: true,
  });
});
onBeforeUnmount(() => {
  if (carousel) {
    carousel.destroy();
  }
});
</script>

<template>
  <h1
    class="container mx-auto text-4xl text-center text-white bg-gradient-to-r from-indigo-500 via-sky-500 to-emerald-500 py-5 px-10 font-bold rounded-lg"
  >
    Flickity Carousel
  </h1>
  <div class="mx-auto m-10 items" id="carousel">
    <div
      class="item bg-center bg-cover bg-no-repeat rounded-lg"
      :style="`background-image:url(${item})`"
      v-for="(item, index) in items"
      :key="index"
    ></div>
  </div>

  <div class="flex justify-center items-center gap-3">
    <input
      v-model="newItem"
      type="text"
      class="w-96 p-3 border-none rounded-lg focus:outline-none italic"
      placeholder="Put a Image URl link"
      required
    />

    <button
      @click="addNewItem()"
      type="button"
      class="inline-flex items-center px-5 py-2 text-sm font-medium text-center text-gray-900 bg-white border border-gray-200 rounded-lg hover:bg-gray-100"
    >
      <span class="text-xl font-bold mr-2"> + </span>
      Add New Image
    </button>
  </div>
</template>

<style scoped>
.items {
  width: 1000px;
  height: 400px;
}
.item {
  width: 1000px;
  height: 400px;
}
</style>
