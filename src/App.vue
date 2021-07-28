<template>
  <div id="app">
    <Header/>
    <NavBar/>
    <Content/>
  </div>
</template>

<script>
import NavBar from '../src/components/layout/theNavBar.vue'
import Header from '../src/components/layout/theHeader.vue'
import Content from '../src/components/layout/theContent.vue'
export default {
  name: 'App',
  components: {
    NavBar,
    Header,
    Content
  }
}
</script>

<style>
  /* @import url("../css/common/main.css"); */
  @import '../src/css/common/main.css';
  @import '../src/css/common/header.css';
  @import '../src/css/common/navbar.css';
  @import '../src/css/common/content.css';  
  @import '../src/css/common/dropdown.css';  
</style>
