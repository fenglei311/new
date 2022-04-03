<template>
	<view class="q">
		<view class="All">
			<view class="content" v-for="(item,index) in navList" :key="index" >
				<view :class="{'active':isActive === index}" @click="checked(index)">
					{{item.title}}
				</view>
			</view>
		</view>
			<view v-if="isActive==0" class="shuaxin1">
				<view>
					<swiper indicator-dots circular autoplay interval="30000">
						<swiper-item>
							<image src="https://n.sinaimg.cn/default/2fb77759/20151125/320X320.png" class="IMG" mode=""></image>
						</swiper-item>
						<swiper-item>
							<image src="https://n.sinaimg.cn/default/2fb77759/20151125/320X320.png" class="IMG" mode=""></image>
						</swiper-item>
					</swiper>
				</view>
				<view
				class="list flex"
				v-for="(item, index) in list"
				:key="index"
				@click="goto(item.uniquekey)"
				>
					<img class="list-img" :src="item.thumbnail_pic_s" alt="" />
					<view class="flex1">
						<p class="two-txt mb10 c-f33">{{ item.title }}</p>
						<p class="c-f99">{{ item.date }}</p>
					</view>
				</view>
				<button class="shuaxin" @click="fresh()">shua</button>
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

	
	export default {
		data() {
			return {
				key:"98226f8d6b2c89432222edbbc5108336",//c1b93684036fe861e84f20008c597565
				order:1,
				lastorder:50,
				page:0,
				list:[],
				isActive: 0,
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
		onLoad() {
			uni.startPullDownRefresh();
		},
		onPullDownRefresh() {
			console.log('触发下拉刷新');
			// setTimeout(()=>{
			// 	this.diaoyong()
			// 	//关闭下拉刷新
			// 	uni.stopPullDownRefresh();
			// },1000)
			this.list = [],
			this.diaoyong()
			setTimeout(function () {
				uni.stopPullDownRefresh();
			}, 1000);
		},
		onShow(){
			this.order = 1,
			this.lastorder = 50,
			this.order = [],
			this.diaoyong()
		},
		onReachBottom() {
			this.order ++
			if(this.order > this.lastorder){
				uni.showToast({
					title:"最后一页"
				})
				return
			}
			// this.list = [],
			this.diaoyong()
		},
		methods: {
			fresh(){
				uni.startPullDownRefresh()
			},
			checked(index) {
				this.isActive = index
			},
			goto(uniquekey) {
				// if (!url) return this.$toast("当前新闻暂无链接！！");
				// location.href = url;
				console.log(uniquekey)
				uni.navigateTo({
					url:'content?uniquekey='+uniquekey
				})
			},
			diaoyong(){
				uni.request({
				    url: '/news', //仅为示例，并非真实接口地址。
				    data: {
						key: this.key,
						page: this.page,
						page_size: 30,
						is_filter:1
				    },
				    header: {
				        'custom-header': 'hello' //自定义请求头信息
				    },
				    success: (res) => {
				        console.log(res.data.result.data);
						// this.list = res.data.result.data
						this.list = this.list.concat(res.data.result.data)
				    }
				});
			},
		},
	}
</script>

<style>
	.IMG{
		width: 375px;
		height: 150px;
	}
	/* 标签页 */
	.All{
		display: flex;
		justify-content: center;
		align-items: center;
		margin-top: 3%;
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
		margin-bottom: 6rpx;
	}
	
	/* 内容 */
	
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
	.shuaxin{
		position: fixed;
		z-index: 2;
		border-radius: 100%;
		background-color: lightgrey;
		width: 50px;
		height: 50px;
		margin: 300px 0 0 300px;
	}
	
/* 	.icon_flushed{
		float: right-botton;
		
	} */
	
	/* 如果宽度是由内容自适应撑开的，则overflow: auto;
	   内容自动撑开容器的宽度不包括滚动条，相当于滚动条是一个和内容并列显示的组件。则
	    overflow-y: scroll;
	*/
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
	.mr50{
		margin-right: 50px;
	}
	
	/* 强制改变（优先权） */
	.mb0 {
	  margin-bottom: 0 !important;
	}
	
	.mb17 {
	  margin-bottom: 17px;
	}
	
	.mb10 {
	  margin-bottom: 20px;
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
	
	
	
	/* 第二行没展示完的字用。。。代替钓 */
	.two-txt {
	  text-overflow: -o-ellipsis-lastline;
	  overflow: hidden;
	  text-overflow: ellipsis; 
	  display: -webkit-box;
	  -webkit-line-clamp: 2;
	  line-clamp: 2;
	  -webkit-box-orient: vertical;
	}
		
</style>
