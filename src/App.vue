<template>
  <Description />
  <Translator />
  <Table />
  <Footer />
</template>

<script>
import Translator from './components/Translator.vue'
import Description from './components/Header.vue'
import Table from './components/Table.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Translator,
    Description,
    Table,
    Footer
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
}
body {
  margin: 0;
}
</style>
