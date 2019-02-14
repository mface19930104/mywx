<template>
  <div class="home">
    <swiper  autoplay="true"   interval="3000" indicator-dots="true "  circular="true" class="slide" >
  <swiper-item v-for="item in slides" :key="item.id">
    <image mode="aspectFill" :src="item.image"></image>
  </swiper-item>
 
</swiper>
<view class="grids">
  <navigator class="item" v-for="item in categories" :key="item.id" :url="'/pages/list/main?id='+item.id">
      <image :src="item.icon"></image>
      <text>{{item.name}}</text>
  </navigator>
</view>
  </div>
</template>
<script>
export default {
  data:()=>({
    slides:[],
    categories:[]
  }),
  created(){
    this.getdata();
    this.getcategory()
  },
  methods:{ 
    getdata () {
      this.$httpWX.get({
        url: 'slides'
      }).then((res) => {
        console.log(res);
        this.slides=res
        console.log(this.slides);
        
      })
    },
    getcategory(){
      this.$httpWX.get({
        url:'categories'
      }).then((res)=>{
           console.log(res);
            this.categories=res
      })
    }
  } 
 } 
</script>
<style lang="less">
.slide{
  height: 380rpx;
}
swiper image{
  width: 100%;
  height: 100%;
}
.grids{
  /* 父盒子采用flex布局横向排列 */
  display: flex;
    /* 父盒子采用flex布局横向排列，但页面宽度不够 就会压缩每个元素宽度 所以为了达到3个一行 需要换行 */
  flex-wrap: wrap;
  border-left: 1rpx solid #ccc;
  border-top: 1rpx solid #ccc;
  box-sizing: border-box;
}
.grids .item {
  /* 每一格设为flex布局 */
  display: flex;
  /* 主轴方向设为竖轴 */
  flex-direction: column;
  justify-content: center;
  align-items:center;
  /* 设置了33.333% */
  width: 33.333%;
  height: 250rpx;
  border-right: 1rpx solid #ccc;
  border-bottom: 1rpx solid #ccc;
  box-sizing: border-box;
}
.grids .item image{
 
  width: 70rpx;
  height: 70rpx;
}
.grids .item text{
  margin: 20rpx;
  display: block;
  font-size: 16px;
}
</style>
