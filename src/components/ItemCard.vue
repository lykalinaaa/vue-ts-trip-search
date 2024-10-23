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
    <p class="for"> за экскурсию</p>
  </section>
</template>

<style scoped>
  .item {
    width: 345px;
    font-family: 'PT Sans Caption';
    color: #444444;
  }

  .trip_img {
    width: 100%;
    border-radius: 5px;
  }

  .rate {
    font-size: 14px;
    font-weight: 400;
  }

  .reviews, .for{
    font-size: 12px;
    font-weight: 400;
    color: #999999;
  }

  .name {
    font-size: 16px;
    font-weight: 700;
  }

  .price {
    font-size: 22px;
    font-weight: 700;
    margin-bottom: 5px;
  }

  .for {
    margin-top: 0px;
  }

  .rating span {
    margin-left: 10px;
  }
</style>
