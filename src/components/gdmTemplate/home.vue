<template>
    <div class="g_content"> 
      <my-header></my-header> 
      <my-list ref='gdmHome'></my-list>
    </div>
</template>

<script>
import MyHeader from '../commonTemplate/header'
import MyList from './hiList'
export default {
  data () {
        
  },
  components: {
    MyHeader,
    MyList,     
  } 

}
</script>
<style scoped>
    @import '../../../static/css/linkstars-search.css'
</style>








