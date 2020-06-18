<template>
  <div id="app">
    <NavBar/>
    <Content msg="This is just a test"/>
    <Footer/>
  </div>
</template>

<script>
import NavBar from './components/NavBar.vue'
import Content from './components/Content.vue'
import Footer from './components/Footer.vue'

export default {
  name: 'App',
  components: {
    NavBar,
    Content,
    Footer
  }
}
</script>
