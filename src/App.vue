<template>
  <div id="app">
    <card-page />
  </div>
</template>

<script>
import CardPage from './pages/CardPage.vue';

export default {
  name: "App",
  components: {
    CardPage
  }
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
