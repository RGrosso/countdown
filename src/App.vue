<template>
  <div id="app">
    <h1>COUNTDOWN APP</h1>  
    <CounterManager/>
  </div>
</template>

<script>
import CounterManager from './components/CounterManager.vue'

export default {
  name: 'App',
  components: {
    CounterManager
  }
}
</script>

<style>

body {
   font-family:Arial, Helvetica, sans-serif;
}

h1 {
  text-align: center;
  font-size: 46px;
}
</style>
