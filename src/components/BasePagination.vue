<template>
  <ul class="list pagination__list list-reset">
    <li class="pagination__item">
      <a class="pagination__link" :class="{ 'pagination__link--disabled': currPage === 1 }"
      @click="prevPage"
        @keypress="prevPage">
        Previous
      </a>
    </li>
    <li class="pagination__item">
      <p style="margin: 0;color: #d1d1d1;">
        {{ props.page }}
      </p>
    </li>
    <li class="pagination__item">
      <a class="pagination__link" :class="{ 'pagination__link--disabled': currPage === pages }"
      @click="nextPage"
        @keypress="nextPage">
        Next
      </a>
    </li>
  </ul>
</template>

<script setup>
import { ref, computed } from 'vue';

const props = defineProps({
  dataInfo: Object,
  page: Number,
});

const emits = defineEmits(['update:page']);

const currPage = ref(1);

const pages = computed(() => props.dataInfo ? props.dataInfo.pages : 0);

const prevPage = () => emits('update:page', currPage.value -= 1);
const nextPage = () => emits('update:page', currPage.value += 1);
</script>
