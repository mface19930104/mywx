<template>
  <div>
  <div v-if="infolist">
     <!-- <view class="listbox">
 <view class="itembox" v-for="item in infolist" :key="item.id" >
  <image src="/static/123.jpg" mode="aspectFill"></image>
  <view class="iteminfo">
    <text class="title">{{item.name}}</text>
    <text>电话：{{item.phone}}</text>
    <text>地址：{{item.address}}</text>
    <text>营业时间：{{item.businessHours}}</text>
  </view>
  <view class="count">
    <view class="countnum">{{item.score}}</view>
  </view>
 </view>
</view> -->
<!-- 微信项目 -->
<view class="cells">
  <navigator class="item" v-for="item in infolist"  :key="item.id" >
    <image src="/static/123.jpg" mode="aspectFill"/>
    <view class="meta">
      <text class="name">{{item.name}}</text>
      <text class="phone">电话：{{item.phone}}</text>
      <text class="address">地址：{{item.address}}</text>
      <text class="hours">营业时间：{{item.businessHours}}</text>
    </view>
    <view class="score">{{item.score}}</view>
  </navigator>
</view>
 <view class="loadmore loading">正在加载。。。</view>
  </div>
  </div>
</template>
<script>
export default {
  data:()=>({
    id:'',
    infolist:''
  }),
  methods:{
     getlist(){
       this.$httpWX.get({
         url:'categories/'+this.id+'/shops',
          data:{
            _page:1,
            _limit:8,
          }
       }).then((res)=>{
        console.log(res);
        this.infolist=res
         console.log(this.infolist);
       })
     }
  },
mounted(){
 this.id=this.$root.$mp.query.id;
   this.getlist()
},
 onReachBottom() {
      console.log('searchScrollLower')
    }
}
</script>
<style lang="less">
.cells {
  background-color: #fff;
}

.cells .item {
  display: flex;
  align-items: flex-start;
  border-bottom: 1rpx solid #eee;
}

.cells .item image {
  width: 160rpx;
  height: 160rpx;
  margin: 20rpx;
}

.cells .item .meta {
  display: flex;
  flex-direction: column;
  flex: 1;
  padding: 10rpx 0;
  font-size: 30rpx;
}

.cells .item .meta .name {
  color: #234;
  font-size: 28rpx;
}

.cells .item .meta .phone,
.cells .item .meta .address {
  color: #678;
  font-size: 24rpx;
}

.cells .item .meta .hours {
  /*color: #ff69b4;*/
  color: #456;
  font-size: 22rpx;
}

.cells .item .score {
  margin: 20rpx 20rpx 0 -40rpx;
  padding: 0 10rpx;
  background-color: #ee523d;
  border-radius: 30rpx;
  color: #fff;
  font-size: 24rpx;
  text-align: center;
}

// .itembox{
//   width: 100%;
//   padding: 10rpx;
//   display: flex;
//   border-bottom: 1rpx solid #eee;
//   box-sizing: border-box;
// }
// .itembox image{
//   height: 100rpx;
//   width: 100rpx
// }
// .iteminfo{
//   display: flex;
//   flex-direction: column;
//   font-size: 22rpx;
//   line-height: 20px;
//   margin-top: 2rpx;
  
// }
// .iteminfo .title{
//   font-size: 14px;
// }
// .count{
//   flex: 1;
//   text-align: right;
 
//   margin-right:30rpx; 
 
//   margin-top: 10rpx;
//   position: relative;
// }
// .count .countnum{
//   position: absolute;
//   right: 0;
//  width: 70rpx;
//  border-radius: 20rpx;
//  height: 40rpx;
//  text-align: center;
//  background-color: #EA4E39;
//  font-size: 14px;
//  color: aliceblue
// }
</style>
