<template>
  <div id="app">
    <Header /> 
    <Main />
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import Header from './components/Header.vue'; 
import Main from './components/Main.vue';

export default defineComponent({
  components: {
    Header,
    Main 
  }
});
</script>

<style lang="scss">
  body {
    background-color: #F8F8FF;
    margin: 0;
    font-family: "Noto Sans", sans-serif;
  }

  #app {
    margin: 0 auto;
    max-width: 1440px;
  }
</style>
