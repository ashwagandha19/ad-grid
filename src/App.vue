<template>
  <div id="app">
    <grid-test></grid-test>
  </div>
</template>

<script>
import GridTest from './components/GridTest.vue'

export default {
  name: 'App',
  components: {
    GridTest,
  }
}
</script>

<style>
body {
  height:100vh;
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: aqua;
}
</style>
