<template>
  <div id="app">
    <Header/>
    <NavBar/>
    <Content/>
    <ModalBox>
    </ModalBox>
    
  </div>
</template>

<script>
import NavBar from '../src/components/layout/theNavBar.vue'
import Header from '../src/components/layout/theHeader.vue'
import Content from '../src/components/layout/theContent.vue'
// import HeaderModal from '../src/components/ModalBox/TheHeaderModal.vue'
// import NavbarModal from '../src/components/ModalBox/TheNavbarModal.vue'
import ModalBox from '../src/components/ModalBox/TheModal.vue'
export default {
  name: 'App',
  components: {
    NavBar,
    Header,
    Content,
    ModalBox
  }
}
</script>

<style>
  /* @import url("../css/common/main.css"); */
  @import '../src/css/common/main.css';
   @import '../src/css/common/text-align.css';
  @import '../src/css/common/header.css';
  @import '../src/css/common/navbar.css';
  @import '../src/css/common/content.css';  
  @import '../src/css/common/dropdown.css';
  @import '../src/css/page/page-infor/main.css';
  @import '../src/css/page/page-infor/header.css'; 
  @import '../src/css/page/page-infor/menu.css'; 
   @import '../src/css/page/page-infor/content.css';
    @import '../src/css/page/page-infor/footer.css';  
</style>
