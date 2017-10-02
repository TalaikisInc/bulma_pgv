<template>
  <div>
    <header-component></header-component>
    <nuxt/>
    <footer-component></footer-component>
  </div>
</template>

<script>
import Footer from '../components/Footer.vue'
import Header from '../components/Header.vue'

export default {
  name: 'mainLayout',
  data () {
    return { }
  },
  components: {
    'footer-component': Footer,
    'header-component': Header
  }
}
</script>

<style>
</style>