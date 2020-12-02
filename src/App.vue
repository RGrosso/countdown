<template>
  <div id="app">
    <h1>COUNTDOWN APP</h1>  
    <Counter 
    :year="2020"
    :month="11"
    :date="25"
    :hour="23"
    :minute="0"
    :second="0"
    :ms="0"
    />
    <Counter 
    :year="2021"
    :month="11"
    :date="25"
    :hour="23"
    :minute="0"
    :second="0"
    :ms="0"
    />
     <Counter 
    :year="2020"
    :month="10"
    :date="25"
    :hour="23"
    :minute="0"
    :second="0"
    :ms="0"
    />
  </div>
</template>

<script>
import Counter from './components/Counter.vue'

export default {
  name: 'App',
  components: {
    Counter
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
