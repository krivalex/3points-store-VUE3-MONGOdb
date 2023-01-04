<template>
  <div id="app">
    <NavbarMain />
    <ContentMain />
    <FooterMain />


  </div>
</template>

<script>
import NavbarMain from './components/NavbarMain.vue'
import FooterMain from './components/FooterMain.vue'
import ContentMain from './components/ContentMain.vue'



export default {
  name: 'App',
  components: {
    NavbarMain,
    FooterMain,
    ContentMain
  }
}
</script>

<style>

</style>
