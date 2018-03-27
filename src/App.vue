<template>
  <div id="app">
    <m-header :seller="seller"></m-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to="/goods">商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/ratings">评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to="/seller">商家</router-link>
      </div>
    </div>
    <router-view :seller="seller"></router-view>
  </div>
</template>

<script>
import MHeader from "components/header/header";
const ERR_OK=0;

export default {
  data(){
    return{
      seller:{
      }
    };
  },
  created(){
    this.$http.get('/api/seller').then((response)=>{
      response=response.body;
      if (response.errno===ERR_OK){
        this.seller=response.data;
      }
    })
  },
  components: {
    MHeader
  },
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "./common/stylus/mixin.styl"
.tab
  display flex
  width: 100%
  height:40px
  border-1px(#ccc)
  .tab-item
    flex 1
    text-align center
    line-height 40px
    & > a
      text-decoration none
      display block
      font-size 14px
      color: rgb(77,85,93)
      &.active
        color: rgb(240,20,20)
</style>
