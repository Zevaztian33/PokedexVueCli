<template>
  <div id="app">
    <Header />
    <Section />
    <Footer />
  </div>
</template>

<script>
import Header from './components/Header.vue'
import Section from './components/Section.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    Header,
    Section,
    Footer,
    
  }
}
</script>

<style>
  body{
    margin: 0;
    padding: 0;
    box-sizing: border-box;
    -webkit-box-sizing: border-box;
    -moz-box-sizing: border-box;
  }
</style>
