<template>
  <label>
    <select style="margin-right: 5px;" name="select-page" v-model="updateNumberPage">
      <option :value="numberPage" v-for="numberPage in pages" :key="numberPage">
        {{ numberPage }}
      </option>
    </select>
    <span style="color: #d1d1d1;">Select number page</span>
  </label>
</template>

<script setup>
import { computed } from 'vue';

const props = defineProps({
  page: Number,
  dataInfo: Object,
});

const emits = defineEmits(['update:page']);

const pages = computed(() => props.dataInfo ? props.dataInfo.pages : 0);

const updateNumberPage = computed({
  get: () => props.page,
  set: (val) => emits('update:page', val),
});
</script>
