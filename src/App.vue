<template> 
  <ApiCall />
</template>

<script>
import ApiCall from './components/ApiCall.vue';

export default {
  name: 'App',
  components: {
    ApiCall
  }
}
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
