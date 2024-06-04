<template>
  <form class="form heroes__form" @submit.prevent="submit" @keydown.ctrl="submit">
    <label class="form__label">
      <input class="form__input" type="text"
      placeholder="Input hero name" name="hero-name" v-model="currName">
    </label>
    <label class="form__label">
      <select class="form__select" v-model="currStatus">
        <option value="Alive">
          Alive
        </option>
        <option value="Dead">
          Dead
        </option>
        <option value="unknown">
          unknown
        </option>
      </select>
    </label>
    <button class="form__btn-submit btn-reset" :class="{ 'btn-offset': currName || currStatus }">
      Applying
    </button>
    <button class="form__button-reset btn-reset" v-if="currName || currStatus"
    @click="reset">
      Reset filters
    </button>
  </form>
</template>

<script setup>
import { ref } from 'vue';

const emits = defineEmits(['update:name', 'update:status', 'update:page']);

const currName = ref('');
const currStatus = ref('');
const currPage = ref(1);

const submit = () => {
  emits('update:name', currName.value);
  emits('update:status', currStatus.value);
  emits('update:page', currPage.value);
};

const reset = () => {
  emits('update:name', currName.value = '');
  emits('update:status', currStatus.value = '');
  emits('update:page', currPage.value);
};
</script>
