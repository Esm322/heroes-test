<template>
  <ul class="list heroes__list list-reset">
    <HeroItem v-for="hero in props.heroes"
    :key="hero.id"
    :name="hero.name"
    :image="hero.image"
    :status="hero.status"
    :species="hero.species"
    :location-name="hero.location.name"
    :first-episode="hero.episode[0]"/>
  </ul>
</template>

<script setup>
import HeroItem from './HeroItem.vue';

const props = defineProps({
  heroes: Array,
});
</script>
