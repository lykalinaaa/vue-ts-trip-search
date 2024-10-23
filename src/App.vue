<script lang="ts">
  import City from './models/CitiesModel';
  import Product from './models/ProductsModel';
  import ItemCard from './components/ItemCard.vue';
  import { ref, watch } from 'vue'

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
      city_id: {
        type: Number,
      },
    },
    components: { ItemCard },
    data () {
      return {
        cities: [] as City[],
        products_all: [] as Product[],
        products_filtered: [] as Product[],
        showCatalogue: false,
        cityParam: '0',
        nameParam: '',
        notFound: false,
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
        this.products_all = products;
      })
      .catch((error) => {console.error(error);})
    },
    methods: {
      selectCityParam() {
        this.products_filtered = this.products_all.filter((item) => item.city_id == this.cityParam);
        if (this.products_filtered.length == 0) this.notFound = true;
        else this.notFound = false;
      },

      selectNameParam() {
        if (this.nameParam != ''){
          this.products_filtered = this.products_all.filter((item) => item.title.includes(this.nameParam));
          if (this.products_filtered.length == 0) this.notFound = true;
          else this.notFound = false;
        }
      },

      resetParams() {
        this.notFound = false;
        this.cityParam = '0';
        this.nameParam = '';
      },
    }
  }
  
</script>

<template>
  <header>
    <img src="./assets/pic/logo.png" alt="Логотип компании">
    <h1>Экскурсии по всему миру</h1>
  </header>

  <section class="search">
    
    <div class="filter">
      <input v-model="nameParam" @change="selectNameParam" class="filter__inner" type="text" placeholder="Введите название экскурсии">
      <select v-model="cityParam" @change="selectCityParam" name="city" class="filter__inner">
        <option value="0">Выберите город</option>
        <option v-for="city in cities" :key="city.id" :value="city.id">{{ city.name }}</option>
      </select>
    </div>
    <div v-if="notFound" class="not_found">
      <p>Поиск не дал результатов</p>
      <button @click="resetParams">Сбросить фильтры</button>
    </div>
    <div class="catalogue">
      <ItemCard 
         v-for="product in products_filtered"
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

  .not_found {
    text-align: center;
    margin-top: 150px;
    font-family: 'PT Sans Caption';
    font-weight: 400;
    font-size: 24px;
    color: #000000;
  }

  .not_found button {
    width: 199px;
    height: 40px;
    background-color: #00A7FF;
    font-family: 'PT Sans Caption';
    color: #FFFFFF;
    border: none;
    border-radius: 5px;
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
    margin-bottom: 100px;
  }

  @media screen and (max-width: 760px) {
    .catalogue {
      justify-content: center;
    }
  }

</style>
