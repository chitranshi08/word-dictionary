<template>
  <div id="app">
    <WordDictionary/>
  </div>
</template>

<script>
import WordDictionary from './components/WordDictionary.vue'

export default {
  name: 'App',
  components: {
    WordDictionary
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
}
body{
  background-color:#673ab7;

}
</style>
