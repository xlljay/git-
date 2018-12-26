<template>
    
</template>

<script>
import $ from 'jquery'
export default {
  data () {
    return {
      gridData:[],
      totalPage: '',
      total: '',
      searchVal:'香水',
      apiUrl:'http://selector.linkstars.com/search/get_list_ajax'
    }
  },
  created () {
    this.clSearch();    
  },
  methods: {
    clSearch(){//输入框搜索
      let q = this.searchVal;
      //
      var parPdos = $('.left_bar').find('label');
      $.each(parPdos,function(i,o){
        $(this).removeClass('checked');
      });
      this.$http.get(this.apiUrl, { params:{q: q}}).then(function(response){         
        if(response.body.error_code == 1000){
          this.gridData = response.body.data.rows;
          this.totalPage = response.body.data.maxpage;
          this.total = response.body.data.total;

          this.$parent.$refs.gdmHome.gridData = this.gridData;
          this.$parent.$refs.gdmHome.searchVal = this.searchVal;
          this.$parent.$refs.gdmHome.totalPage = this.totalPage;
          this.$parent.$refs.gdmHome.total = this.total;

        } else if(response.body.error_code == 1001){
          console.log('没输入关键词')          
        } else if(response.body.error_code == 1002){
          this.aError = true
          console.log('没有相关产品')
        }       
        
      },function(){
        console.log('服务器返回错误')
      })
      
      
    },

  }
}
</script>

