<template>
<div>
  <ul>
    <answers-layout
      v-for="res in resources"
      :key="res.id"
      :id="res.id"
      :prompt="res.prompt"
      :response="res.response"
      :link="res.link"
    ></answers-layout>
  </ul>
  </div>
</template>

<script>
import AnswersLayout from './AnswersLayout.vue';

export default {
  inject: ['resources'],
  components: {
    AnswersLayout
  }
};
</script>

<style scoped>
ul {
  list-style: none;
  margin: 0;
  padding: 0;
  margin: auto;
  max-width: 40rem;
}
</style>
