<template>
	<view>
		<view class="All">
			<view class="content" v-for="(item,index) in navList" :key="index" >
				<view :class="{'active':isActive === index}" @click="checked(index)">
					{{item.title}}
				</view>
			</view>
		</view>
		<view v-if="isActive==0">
			<view class="title" v-for="(item,index) in list" :key="index">
				<text class="title_title two-txt ml10">
					{{item.title}}
				</text>
				<text class="time">
					{{item.time}}
				</text>
				<video class="title_video ml35" src="https://bjetxgzv.cdn.bspapp.com/VKCEYUGU-uni-app-doc/a876efc0-4f35-11eb-97b7-0dc4655d6e68.mp4" 
				controls
				autoplay
				>
				</video>
				<view class="title_flex">
					<p class="title_text ml10">
						{{item.src}}
					</p>
					<view class="title_icon">
						<uni-icons type="hand-up" size="30" v-show="showUpImg" @click="changeImg">
							
						</uni-icons>
						<uni-icons type="hand-up-filled" size="30" v-show="!showUpImg" @click="changeImg">
							
						</uni-icons>
						<uni-icons type="chat" size="30">
							
						</uni-icons>
						<uni-icons type="more" size="30">
							
						</uni-icons>
					</view>
					
				</view>
				<view class="box">
					
				</view>
			</view>
		</view>
		<view class="content_concern" v-if="isActive==1">
			1
		</view>
		<view class="content_time" v-if="isActive==2">
			2
		</view>
		<view class="content_wait_one" v-if="isActive==3">
			3
		</view>
		<view class="content_wait_two" v-if="isActive==4">
			4
		</view>
	</view>
</template>

<script>
	import news1 from "../first.js"
	
	export default {
		data() {
			return {
				showUpImg:true,
				isActive: 0,
				list:news1,
				navList:[
					{
						index: 0,
						title: '推荐',
						
					},{
						index: 1,
						title: "关注流"
					},{
						index: 2,
						title: "24小时"
					},{
						index: 3,
						title: "等等"
					},{
						index: 4,
						title: "等等"
					}
				],
			}
		},
		methods: {
			checked(index) {
				this.isActive = index
			},
			changeImg(){
				this.showUpImg = !this.showUpImg
			},
		}
	}
</script>

<style>
	.box{
		margin: 20px 0 20px 0;
		width: 100%;
		border-bottom: 1px solid lightgrey;
	}
	/* 标题 */
	.All{
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 3%;
		margin-bottom: 20px;
	}
	.All  .content {
		height: 90rpx;
		line-height: 90rpx;
		width: 100%;
		text-align: center;
		font-size: 32rpx;
		font-family: Alibaba PuHuiTi;
		color: #333;
	}
	.active {
		position: relative;
		color: #1F75FE;
	}
	.active::after {
		content: "";
		position: absolute;
		width: 100rpx;
		height: 4rpx;
		background-color: #1F75FE;
		left: 0px;
		right: 0px;
		bottom: 0px;
		margin: auto;
	}
	
	/* 内容 */
	.title{
		display: flex;
		flex-direction: column;
	}
	.title_title{
		font-weight: 700;
		font-size: 48rpx;
	}
	.title_video{
		
	}
	.title_flex{
		display: flex;
		flex-direction: row;
		justify-content: space-around;
	}
	
	.title_text{
		font-size: 40rpx;
	}
	.title_icon{
		float: right;
	}
	
	.time{
		margin: 5px 0 5px 175px;
	}
	
	
	* {
	  padding: 0;
	  margin: 0;
	}
	.swipe-image {
	  width: 100%;
	  height: 100%;
	}
	.box {
	  font-size: 14px;
	}
	.van-tabs__content {
	  height: calc(100vh - 140px);
	  overflow-y: scroll;
	}
	.head {
	  height: 45px;
	  background-color: #3480ff;
	  padding: 0 10px;
	  color: #ffffff;
	}
	.van-tabs__line {
	  background-color: #3480ff !important;
	}
	.list {
	  padding: 10px;
	  border-bottom: 1px solid #e1e1e1;
	}
	.list-img {
	  height: 66px;
	  width: 100px;
	  margin-right: 20px;
	}
	.foot {
	  position: absolute;
	  width: 100%;
	  bottom: 0;
	  height: 50px;
	  justify-content: space-around;
	  background-color: #f4f6f8;
	}
	.my-swipe .van-swipe-item {
	  color: #fff;
	  font-size: 20px;
	  line-height: 120px;
	  height: 120px;
	  text-align: center;
	  background-color: #39a9ed;
	}
	.van-pull-refresh {
	  height: 100%;
	}
	
	/* 弹性盒 */
	.flex {
	  display: flex;
	}
	
	.flex1 {
	  flex: 1;
	}
	
	.flex2 {
	  flex: 2;
	}
	
	.flex-space-between {
	  justify-content: space-between;
	}
	
	.flex-align-center {
	  align-items: center;
	}
	
	.flex-direction-column {
	  flex-direction: column;
	}
	
	.flex-center {
	  justify-content: center;
	}
	
	.flex-direction-r {
	  flex-direction: row-reverse;
	}
	
	.space-between {
	  justify-content: space-between;
	}
	
	.space-around {
	  justify-content: space-around;
	}
	
	.space-center {
	  justify-content: center;
	}
	.mt10 {
	  margin-top: 10px;
	}
	
	.mt20 {
	  margin-top: 20px;
	}
	
	.mt30 {
	  margin-top: 30px;
	}
	
	.mr10 {
	  margin-right: 10px;
	}
	
	.mr30 {
	  margin-right: 30px;
	}
	
	.mb0 {
	  margin-bottom: 0 !important;
	}
	
	.mb17 {
	  margin-bottom: 17px;
	}
	
	.mb10 {
	  margin-bottom: 10px;
	}
	
	.mb15 {
	  margin-bottom: 15px;
	}
	
	.mb20 {
	  margin-bottom: 20px;
	}
	
	.mb30 {
	  margin-bottom: 30px;
	}
	
	.mb40 {
	  margin-bottom: 40px;
	}
	
	.ml10 {
	  margin-left: 10px;
	}
	
	.ml20 {
	  margin-left: 20px;
	}
	
	.ml30{
		margin-left: 30px;
	}
	
	.ml35{
		margin-left: 35px;
	}
	
	.ml50{
		margin-left: 50px;
	}
	.ml200{
		margin-left: 200px;
	}
	
	.pl20 {
	  padding-left: 20px;
	}
	
	.pr20 {
	  padding-right: 20px;
	}
	
	.c-404040 {
	  color: #404040;
	}
	
	.c-ff {
	  color: #ffffff;
	}
	
	.c-f66 {
	  color: #666;
	}
	
	.c-f88 {
	  color: #888;
	}
	
	.c-f33 {
	  color: #333;
	}
	
	.c-f99 {
	  color: #999;
	}
	
	.c-f252B3A {
	  color: #252b3a;
	}
	
	.c-1D939A {
	  color: #1d939a;
	}
	
	.f12 {
	  font-size: 12px;
	}
	
	.f14 {
	  font-size: 14px;
	}
	
	.f16 {
	  font-size: 16px;
	}
	
	.f18 {
	  font-size: 18px;
	}
	
	.f24 {
	  font-size: 24px;
	}
	
	.f26 {
	  font-size: 26px;
	}
	
	.f30 {
	  font-size: 30px;
	}
	
	.f36 {
	  font-size: 36px;
	}
	
	.fw400 {
	  font-weight: 400;
	}
	
	.fw700 {
	  font-weight: 700;
	}
	
	.tc {
	  text-align: center;
	}
	
	.tr {
	  text-align: right;
	}
	
	
	
	.tl {
	  text-align: left;
	}
	
	.abs {
	  position: absolute;
	}
	
	.rel {
	  position: relative;
	}
	
	
	
	/* 没展示完的字用。。。代替 */
	.two-txt {
	  text-overflow: -o-ellipsis-lastline;
	  overflow: hidden;
	  text-overflow: ellipsis;
	  display: -webkit-box;
	  -webkit-line-clamp: 1;
	  line-clamp: 1;
	  -webkit-box-orient: vertical;
	}

</style>
