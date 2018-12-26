<template>
  <div id="app">
   <!--  <router-view></router-view> -->
    <my-home></my-home>       
    <my-footer></my-footer>
  </div>
</template>

<script>
import MyFooter from './components/commonTemplate/footer'
import MyHome from './components/gdmTemplate/home'
import $ from 'jquery'
export default {   
  name:'app',
  data () {
    return {
    } 
  },
  created () {    
  },
  methods:{    
  },      
  components: {
    MyFooter,
    MyHome       
  }  
}
</script>

<style scoped>
  @import '../static/css/base.css';
  @import '../static/css/common.css';
</style>
