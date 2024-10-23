<script lang="ts">
  import City from './models/CitiesModel';
  import Product from './models/ProductsModel';
  import ItemCard from './components/ItemCard.vue';

  export default {
    props: {
      id: {
        type: Number,
      },
      imgSrc: {
        type: String,
      },
      name: {
        type: String,
      },
      rate: {
        type: Number,
      },
      reviews: {
        type: Number,
      },
      price: {
        type: String,
      },
    },
    components: { ItemCard },
    data () {
      return {
        cities: [] as City[],
        products: [] as Product[],
        showCatalogue: false,
      }
    },
    created() {
      fetch('../data/cities.json')
      .then(res => res.json())
      .then(cities => {
        this.cities = cities;
      })
      .catch((error) => {console.error(error);});

      fetch('../data/products.json')
      .then(res => res.json())
      .then(products => {
        this.products = products;
      })
      .catch((error) => {console.error(error);})
    },
  }
  
</script>

<template>
  <header>
    <img src="./assets/pic/logo.png" alt="Логотип компании">
    <h1>Экскурсии по всему миру</h1>
  </header>

  <section class="search">
    
    <div class="filter">
      <input class="filter__inner" type="text" placeholder="Введите название экскурсии">
      <select name="city" class="filter__inner">
        <option value="Выбрать город">Выбрать город</option>
        <option v-for="city in cities" :key="city.id" :value="city.id">{{ city.name }}</option>
      </select>
    </div>
    <div class="catalogue">
      <ItemCard 
         v-for="product in products"
         :id="product.id"
         :imgSrc="product.cover_photo.big"
         :name="product.title"
         :price="product.netto_price"
         :rate="product.customers_review_rating"
         :review="product.reviews"
      />
    </div>
  </section>
</template>

<style scoped>

  header {
    text-align: center;
    margin-top: 50px;
    font-family: 'PT Sans Caption';
    font-weight: 700;
    font-size: 22px;
  }

  header img {
    width: 150px;
  }

  .filter {
    display: flex;
    gap: 30px;
    justify-content: center;
    margin-top: 55px;
    flex-wrap: wrap;
  }

  .filter__inner {
    width: 300px;
    height: 50px;
    border: 1px solid rgba(0,0,0,0.15);
    color: #999999;
    font-size: 16px;
    padding-left: 15px;
  }

  .filter__inner::-webkit-scrollbar {
    display: none;
  }

  .catalogue {
    display: flex;
    flex-wrap: wrap;
    gap: 40px;
    justify-content: left;
    max-width: 1115px;
    margin-top: 70px;
    margin-left: auto;
    margin-right: auto;
  }

</style>
