<template>
  <Description />
  <Translator />
  <Table />
</template>

<script>
import Translator from './components/Translator.vue'
import Description from './components/Header.vue'
import Table from './components/Table.vue'

export default {
  name: 'App',
  components: {
    Translator,
    Description,
    Table
  }
}
</script>

<style>
#app {
  font-family: Verdana, Geneva, Tahoma, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
