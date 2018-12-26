<template>
      <div class="m_content clearfix">
        <div class="left_bar">
          <ul>
            <li>
              <div class="category_all">
                <div class="category_titel clearfix">
                  <h2>筛选类目111111</h2>
                  <span @click='checkedAll($event)'>全部清空</span>
                </div>
              </div>
            </li>
            <li>
              <div class="category_all">
                <div class="category_titel clearfix">
                  <h2>商家地域222</h2>
                  <span @click='checkedSingle($event)'>清空</span>
                </div>                
                <div class="screening_list">
                  <label v-bind:class="['check',{ 'checked' : item.oisChecked }]" @click="getState($event)" v-for="item in oneItems" :id='item.val'>{{ item.ev }}</label>
                </div>             
              </div>
            </li>
            <li>
              <div class="category_all">
                <div class="category_titel clearfix">
                  <h2>商家类型333</h2>
                  <span @click='checkedSingle($event)'>清空</span>
                </div>
                <div class="screening_list">
                  <label v-bind:class="['check',{ 'checked' : item.tisChecked }]" @click="getState($event)" v-for="item in twoItems" :id='item.val'>{{ item.ev }}</label>
                </div> 
              </div>
            </li>
            <li>
              <div class="category_all">
                <div class="category_titel clearfix">
                  <h2>电商商城444</h2>
                  <span @click='checkedSingle($event)'>清空</span>
                </div>
                <div class="screening_merchants">
                  <div class="screening_list">
                    <label v-bind:class="['check',{ 'checked' : item.hisChecked }]" @click="getState($event)" v-for="item in threeItems" :id='item.val'>{{ item.ev }}</label>
                  </div>
                </div>
               
              </div>
            </li>
            <!-- <li>
              <div class="category_all">
                <div class="category_titel clearfix">
                  <h2>商品库存</h2>
                  <span @click='checkedSingle($event)'>清空</span>
                </div>
                <div class="screening_list cl_shu">
                  <label class="check" @click='clSku($event)'>有 </label>
                  <label class="check" @click='clSku($event)'>无</label>
                </div>
              </div>
            </li> -->
            <li>
              <div class="category_all">
                <div class="category_titel clearfix">
                  <h2>价格区间</h2>
                  <span @click='checkedSingle($event)'>清空</span>
                </div>
                <div class="interval_pst clearfix">
                  <div class="pst_left">
                    <em class="nth-oem"></em>
                    <em class="nth-tem"></em>
                    <input type="text" name=""  v-model='priceGt'> <i>—</i>
                    <input type="text" name=""  v-model='priceLt'>
                  </div>
                  <a href="javascript:;" @click='priceSearch'>确定</a>
                </div>
              </div>
            </li>
          </ul>
        </div>
        <div class="stars_list">
          <div class="all_results clearfix">
            <div class="results_left">
              <h3>全部结果</h3>
              <span v-bind:class="{'as_active':aActive}" @click='asActive1($event)'>佣金<i v-bind:class="['nth_fis',{nth_fis_active:aActive}]" ></i></span>
              <span v-bind:class="{'as_active':sActive}" @click='asActive2($event)'>价格<i v-bind:class="['nth_two',{nth_two_active:sActive}]"  ></i></span>
              <!-- <span v-bind:class="{'as_active':aActive}" @click='asActive1'>佣金<i v-bind:class="['nth_fis_active',{nth_asc_active:fActive}]" ></i></span>
              <span v-bind:class="{'as_active':sActive}" @click='asActive2'>价格<i v-bind:class="['nth_two',{nth_two_active:sActive}]"  ></i></span> -->
              <span><i v-bind:class="['nth_ser',{nth_ser_active:local}]" @click='isShow1'></i></span>
              <span><i v-bind:class="['nth_fou',{nth_fou_active:slocal}]" @click='isShow2'></i></span>
            </div>
            <div class="results_right">
              总计<i>{{ total }}</i>件相关商品
              <em class="nth_fir" @click='prevPage(currentPage)'></em>
              <i class="s_currentPage">{{ currentPage }}</i>/<i>{{ totalPage }}</i>
              <em class="nth_seg" @click='nextPage(currentPage)'></em>
            </div>
          </div>
          <div class="error" ><img src="/static/img/error_03.jpg"></div>
          <ul class="dis-project project_list" v-show="this.local">
            <li v-for='(item,index) in gridData'>
              <div class="fis_list clearfix">
                <div class="l_commodity">
                  <a :href='item.Url' target="_blank"><img :src="item.ImageUrl"></a>
                  <span>{{item.WebsiteName}}</span>
                </div>
                <div class="l_standard">
                  <a  :href='item.Url' target="_blank">{{item.Title}}</a>
                  <div class="l_fise">
                    <dl>
                      <dt>参考价格：¥{{item.Price}}</dt>
                      <dd>当前库存：{{item.IsSoldOut}}</dd>
                    </dl>
                    <dl>
                      <dt>参考佣比：{{item.CommissionRate}}%</dt>
                      <dd>参考佣金：¥{{item.RmbPrice}}/件</dd>
                    </dl>
                  </div>                
                </div>
                <a class="to_promote" href="javascript:;">去推广 ></a>
              </div>
            </li>
          </ul>
          <ul class="dis-project project_list_shu clearfix"  v-show='this.slocal'>
            <li v-for='(item,index) in gridData'>
              <div class="fis_list clearfix">
                <div class="l_commodity">
                  <a :href='item.Url' target="_blank"><img :src="item.ImageUrl"></a>
                  <span>{{item.WebsiteName}}</span>
                </div>
                <div class="l_standard">
                  <a  :href='item.Url' target="_blank">{{item.Title}}</a>
                  <div class="l_fise">
                    <dl>
                      <dt>参考价格：¥{{item.Price}}</dt>
                      <dd>当前库存：{{item.IsSoldOut}}</dd>
                    </dl>
                    <dl>
                      <dt>参考佣比：{{item.CommissionRate}}%</dt>
                      <dd>参考佣金：¥{{item.RmbPrice}}/件</dd>
                    </dl>
                  </div>                
                </div>
                <div class="m_cen">
                  <a class="to_promote" href="javascript:;">去推广 ></a>
                </div>              
              </div>
            </li>          
          </ul>
        </div>
      </div>
</template>

<script>
import $ from 'jquery'
export default {
  data () {
    var businessArea = {
          '国内商家':'国内',
          '海外商家':'海外',
          '跨域商家':'跨境'
        };
    var businessType = {
        '品牌商':'品牌型',
        '综合电商':'综合型',
        '垂直电商':'垂直型'
    };
    var electricityMall = {
        '京东':'1',
        '新蛋':'2',
        '苏宁易购':'17',
        '当当':'24',
        '国美':'70',
        '天猫商城':'71',
        '亚马逊中国':'96',
        '顺丰优选':'102',
        '中粮我买网':'103'
    };
    var oneArray = [];
    var twoArray = [];
    var threeArray = [];
    $.each(businessArea, function(i,o){
      var a = { ev : i, oisChecked : false, val: o}
      oneArray.push(a);
    })
    $.each(businessType, function(i,o){
      var a = { ev : i, tisChecked : false, val: o}
      twoArray.push(a);
    })
    $.each(electricityMall, function(i,o){
      var a = { ev : i, hisChecked : false, val: o}
      threeArray.push(a);
    })    
    return { 
      oneItems: oneArray, 
      twoItems: twoArray, 
      threeItems: threeArray,  
      fisChecked: false,   
      searchVal:$('.m_search input').val(),
      priceLt:'',//小于
      priceGt:'',//大于
      gridData:[],      

      apiUrl:'http://selector.linkstars.com/search/get_list_ajax',//test/get_item_info
      local: true,
      slocal: false,
      aActive: true,
      sActive: false,
      aError: true,
      currentPage: '1',
      totalPage: '',
      total: '',
      area:[],
      type:[],
      webids:[]
    }
        
  },
  created () {    
    $(window).scroll(function(){
      var topOffset = $('.left_bar').offset().top;
      var scrollTop = $(document).scrollTop();
      if (scrollTop > topOffset){
          $('.left_bar').css({
              top: 0,
              position: 'fixed',
          });
      } 

      if (topOffset < 80){
          $('.left_bar').css({
              top: 0,
              position: 'relative',
          });
      }
    });    
  },
  methods:{
    clSku(event){      
      var thisNode = event.currentTarget;
      $(".cl_shu label").removeClass("checked"); 
      $(thisNode).addClass("checked");
    },  
    a(){
           var res = [];
           var json = {};
           for(var i = 0; i < this.length; i++){
            if(!json[this[i]]){
             res.push(this[i]);
             json[this[i]] = 1;
            }
           }
           return res;        
      
    },        
    getState:function(event){ 
      let thisNode = event.currentTarget;
      let ind = this.index(thisNode,thisNode.parentNode.getElementsByTagName('label'));
      let _this =this;
      if($(thisNode).parent().prev().find('h2').text() == '商家地域'){
        this.oneItems[ind].oisChecked = !this.oneItems[ind].oisChecked;
        _this.area = [];
        this.oneItems.forEach(function(arr,index){
          if (arr.oisChecked){
            _this.area.push(arr.val);
          }
        })
        
      }
      if($(thisNode).parent().prev().find('h2').text() == '商家类型'){
        this.twoItems[ind].tisChecked = !this.twoItems[ind].tisChecked;
        let _this =this; 
        _this.type = [];
        this.twoItems.forEach(function(arr,index){
          if (arr.tisChecked){
            _this.type.push(arr.val);
          }
        })
      }
      if($(thisNode).parent().parent().prev().find('h2').text() == '电商商城'){
        this.threeItems[ind].hisChecked = !this.threeItems[ind].hisChecked;
        let _this =this; 
        _this.webids = [];
        this.threeItems.forEach(function(arr,index){
          if (arr.hisChecked){
            _this.webids.push(arr.val);
          }
        })
      }      
            
      let gridData = [];
      this.$http.get(this.apiUrl, { params: {q:this.searchVal, area: this.area.join(','),type:this.type.join(','), webids: this.webids.join(','), page: this.currentPage}}).then(function(response){ 
            if(response.body.error_code == 1000){
              this.gridData = response.body.data.rows;
              this.currentPage = 1;
              // $('.error').css({'display':'none'});
              // $('.project_list_shu').css({'display':'inline-block'});
            } else if(response.body.error_code == 1001){
              alert('没输入关键词')          
            } else if(response.body.error_code == 1002){
              $('.error').css({'display':'inherit'});
              $('.project_list').css({'display':'none'});
              console.log('没有相关产品')
            }        
            
        },function(){
            console.log('服务器返回错误')
        })

    },
    index:function(current, obj){ 
      for (var i = 0, length = obj.length; i<length; i++) { 
        if (obj[i] == current) { 
          return i; 

        } 
      } 
    },
    priceSearch(){//价格区间搜索
      let priceGt = this.priceGt;//大于
      let priceLt = this.priceLt;//小于
      if($('.pst_left input').val() == ''){
        alert('价格区间不能为空')
      }
      if(priceGt > priceLt){
        alert('请填写正确区间价格')
      } else{
        this.$http.get(this.apiUrl, { params: {q:this.searchVal, priceGt: priceGt, priceLt:priceLt}}).then(function(response){        
          this.gridData = response.body.data.rows;
        },function(){
          console.log('服务器返回错误')
        })
      }
      
    },
    checkedAll(event){//清空（全部）
      var _this = event.currentTarget
      var parPdos = $(_this).parents('ul').find('label');
      if(parPdos.hasClass('checked')){
        this.$http.get(this.apiUrl, { params: {q:this.searchVal}}).then(function(response){ 
            if(response.body.error_code == 1000){
              this.gridData = response.body.data.rows;
              this.currentPage = 1;
            }      
            
        },function(){
            console.log('服务器返回错误')
        })
      } 
      $.each(parPdos,function(i,o){
        $(this).removeClass('checked');
      });           
      
      $('.pst_left input').val('');
    },
    checkedSingle(event) {//清空（反选）
      var _this = event.currentTarget
      var parPdos = $(_this).parents('li').find('label');
      if(parPdos.hasClass('checked')){      
        this.$http.get(this.apiUrl, { params: {q:this.searchVal}}).then(function(response){ 
            if(response.body.error_code == 1000){
              this.gridData = response.body.data.rows;
              this.currentPage = 1;
            }      
            
        },function(){
            console.log('服务器返回错误')
        }) 
      }
      $.each(parPdos,function(i,o){
        $(this).removeClass('checked');
      }); 

      $('.pst_left input').val('');   
      
    },
    asActive1(event){//佣金
      this.aActive=true;
      this.sActive =false; 
      //this.fActive = true;
      var _this = event.currentTarget
      if($(_this).find('i').hasClass('nth_fis_active')){
        $(_this).find('i').addClass('nth_asc_active');
        $(_this).find('i').removeClass('nth_fis_active');
        console.log('dao')
        this.$http.get(this.apiUrl, { params: {q:this.searchVal,order:'CommissionRate',sort:'desc'}}).then(function(response){         
            this.gridData = response.body.data.rows;        
        },function(err){
          console.log('服务器返回错误')
        })
      } else{        
        $(_this).find('i').addClass('nth_fis_active');
        $(_this).find('i').removeClass('nth_asc_active');
        console.log('zheng')
        this.$http.get(this.apiUrl, { params: {q:this.searchVal,order:'CommissionRate',sort:'asc'}}).then(function(response){         
            this.gridData = response.body.data.rows;        
        },function(err){
          console.log('服务器返回错误')
        })
        
      }
      
           
    },
    asActive2(event){//价格
      this.aActive=false
      this.sActive =true
      var _this = event.currentTarget
      if($(_this).find('i').hasClass('nth_two_active')){
        $(_this).find('i').addClass('nth_asc_active');
        $(_this).find('i').removeClass('nth_two_active');
        console.log('dao')
        this.$http.get(this.apiUrl, { params: {q:this.searchVal,order:'price',sort:'desc'}}).then(function(response){         
            this.gridData = response.body.data.rows;        
        },function(err){
          console.log('服务器返回错误')
        })
      } else{        
        $(_this).find('i').addClass('nth_two_active');
        $(_this).find('i').removeClass('nth_asc_active');
        console.log('zheng')
        this.$http.get(this.apiUrl, { params: {q:this.searchVal,order:'price',sort:'asc'}}).then(function(response){         
            this.gridData = response.body.data.rows;        
        },function(err){
          console.log('服务器返回错误')
        })
        
      }
      // this.$http.get(this.apiUrl, { params: {q:this.searchVal,order:'price',sort:'desc'}}).then(function(response){        
      //   this.gridData = response.body.data.rows;
      // },function(){
      //   console.log('服务器返回错误')
      // })
    },
    isShow1(){//横版
      this.local=true
      this.slocal =false
    },
    isShow2(){//竖版
      this.slocal=true
      this.local = false
    },
    prevPage (num) {//上一页 分页
      console.log(num)
      if(num == 1){
        return
      } else{
        this.currentPage--
      }
      this.$http.get(this.apiUrl, { params: {q:this.searchVal, page: this.currentPage}}).then(function(response){
        this.gridData = response.body.data.rows;        
      },function(){
        console.log('服务器返回错误')
      })
      
    },
    nextPage(num){//下一页 分页
      if(num == this.totalPage){
        return
      } else{
        this.currentPage++
      }
      this.$http.get(this.apiUrl, { params: {q:this.searchVal, page: this.currentPage}}).then(function(response){
        this.gridData = response.body.data.rows;        
      },function(){
        console.log('服务器返回错误')
      })
    } 
  }

}
</script>





