<script lang="ts">
  import City from './models/CitiesModel';
  import ItemCard from './components/ItemCard.vue';

  export default {
    
    data () {
      return {
        cities: [] as City[],
        items: [],
      }
    },
    created() {
      fetch('../data/cities.json')
      .then(res => res.json())
      .then(cities => {
        this.cities = cities;
      })
      .catch((error) => {console.error(error);})
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
      <form>
        <input class="filter__inner" type="text" placeholder="Введите название экскурсии">
      </form>
      <select name="city" class="filter__inner">
        <option value="Выбрать город">Выбрать город</option>
        <option v-for="city in cities" :key="city.id" :value="city.id">{{ city.name }}</option>
      </select>
    </div>
    <div class="catalogue">

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
  }

  .filter__inner {
    width: 300px;
    height: 50px;
    border: 1px solid rgba(0,0,0,0.15);
    color: #999999;
    font-size: 16px;
    padding-left: 15px;
  }



</style>
