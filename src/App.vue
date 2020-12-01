<template>
  <div id="app">
    <Counter 
    :year="2020"
    :month="11"
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
</style>
