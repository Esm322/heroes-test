<template>
  <main>
    <div class="container heroes__container">

      <div class="heroes__wrapper-top">
        <TopPagination
        v-model:page="page"
        :data-info="dataHeroes.info"/>

        <HeroesFilter
        v-model:page="page"
        v-model:name="heroName"
        v-model:status="heroStatus"/>
      </div>

      <HeroesList
      :heroes="dataHeroes.results"/>

      <BasePagination
      v-model:page="page"
      :data-info="dataHeroes.info"/>

    </div>
  </main>
</template>

<script setup>
import {
  ref,
  onMounted,
  watch,
} from 'vue';
import axios from 'axios';

import HeroesList from './components/HeroesList.vue';
import BasePagination from './components/BasePagination.vue';
import HeroesFilter from './components/HeroesFilter.vue';
import TopPagination from './components/TopPagination.vue';

const dataHeroes = ref({});
const page = ref(1);
const heroName = ref('');
const heroStatus = ref('');

const getHeroes = () => {
  return axios.get('https://rickandmortyapi.com/api/character', {
    params: {
      page: page.value,
      name: heroName.value,
      status: heroStatus.value,
    },
  })
    .catch((err) => console.log(err))
    .then((response) => dataHeroes.value = response.data);
};

watch(
  () => page.value,
  (newValue) => {
    if (newValue) {
      getHeroes();
    }
  },
);

watch(
  () => heroStatus.value || heroName.value,
  (newValue) => {
    if (newValue) {
      getHeroes();
    }

    if (newValue === '') {
      getHeroes();
    }
  },
);

onMounted(() => {
  getHeroes();
});
</script>

<style>
@import url('./assets/styles/style.scss');
</style>
