<template>
  <div id="app">
    <TicTacToe />
  </div>
</template>

<script>
import TicTacToe from './components/TicTacToe.vue';

export default {
  name: 'App',
  components: {
    TicTacToe,
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
