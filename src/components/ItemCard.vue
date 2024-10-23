<script setup lang="ts">
  defineProps({
    id: {
      type: Number,
    },
    imgSrc: {
      type: String,
    },
    name: {
      type: String,
    },
    price: {
      type: String,
    },
    rate: {
      type: Number,
    },
    reviews: {
      type: Number,
    },
  })
</script>

<template>
  <section class="item">
    <img class="trip_img" :src="imgSrc" alt="Картинка">
    <div class="rating">
      <img src="../assets/pic/star.png" alt="">
      <span class="rate">{{ rate }}</span>
      <span class="reviews">{{ reviews }}</span>
    </div>
    <p class="name">{{ name }}</p>
    <p class="price"> от {{ price }}</p>
    <p> за экскурсию</p>
  </section>
</template>

<style scoped>
  .item {
    width: 345px;
  }

  .trip_img {
    width: 100%;
  }
</style>
