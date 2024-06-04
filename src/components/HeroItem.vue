<template>
  <li class="list__item">
    <article class="article heroes__article">
      <div class="article__wrapper-img">
        <img class="article__img" :src="props.image" :alt="props.name">
      </div>

      <div class="article__wrapper-text">
        <div class="article__wrapper-lining">
          <a class="article__title link" :href="props.name">
            <h2 class="hero-name">
              {{ props.name }}
            </h2>
          </a>

          <span class="article__race">
            <span :class="[{ 'status-race': props.status === 'Alive' },
            { 'status-race--dead': props.status === 'Dead' },
            { 'status-race--unknown': props.status === 'unknown' }]">
            </span>
            {{ props.status }} - {{ props.species }}
          </span>
        </div>

        <div class="article__wrapper-lining">
          <span class="article__clarification-location text-gray">
            Last known location:
          </span>

          <a class="article__location-desc text-desc link" :href="props.locationName">
            {{ props.locationName }}
          </a>
        </div>

        <div class="article__wrapper-lining">
          <span class="article__clarification-seen text-gray">
            First seen in:
          </span>

          <a href="" class="article__seen text-desc link">
            {{ episode.name }}
          </a>
        </div>
      </div>
    </article>
  </li>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import axios from 'axios';

const props = defineProps({
  name: String,
  image: String,
  status: String,
  species: String,
  locationName: String,
  firstEpisode: String,
});

const episode = ref({});

const getEpisode = () => {
  return axios.get(props.firstEpisode)
    .then((response) => episode.value = response.data);
};

onMounted(() => {
  getEpisode();
});
</script>
