<script setup>
import { RouterView } from 'vue-router'
import GlobalHeader from './components/GlobalHeader.vue';
</script>

<template>
  <GlobalHeader />
  <RouterView />
</template>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Montserrat:ital,wght@0,100..900;1,100..900&family=Rubik:ital,wght@0,300..900;1,300..900&display=swap');

  * {
    font-family: "Rubik", sans-serif;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .container{
    max-width: 1100px;
    margin: 0 auto;
  }

  body{
    background-color: #2c2c2c;
    background-image: url(./assets/);
    background-repeat: no-repeat;
    background-position: center center;
    background-size: cover;
  }
</style>
