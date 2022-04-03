<template>
	<view class="big">
		<city-select
		v-if="iscityshow"
		@cityClick="cityClick"
		:formatName="formatName"
		:activeCity="activeCity"
		:obtainCitys="obtainCitys"
		:isSearch="true"
		ref="citys"
		></city-select>
		<view v-else class="">
			<view class="trade">
				<view class="texts" :class="curr==0?'active':''" data-index="0" @tap="set">
					疫情播报
				</view>
				<view class="texts" :class="curr==1?'active':''" data-index="1" @tap="set">
					出行政策
				</view>
				<view class="texts" :class="curr==2?'active':''" data-index="2" @tap="set">
					检测机构
				</view>
				<view class="texts" :class="curr==3?'active':''" data-index="3" @tap="set">
					风险地区
				</view>
			</view>
			<swiper :disable-touch="istouch" class="swp" style="height: 100vh;" acceleration="false"  :current="curr" @change="set">
				<swiper-item>
					<scroll-view>
						<view class="One_All">
							<view class="zhengzhou">
								<image class="img" :src="src_img" mode="">
								</image>
								<text class="zhengzhou_font">
									{{qq}}
								</text>
								<button @click="showcity()" type="default" class="zhengzhou_botton">
									切换城市
								</button>
							</view>
							<view class="quanqiu">
								<view class="quanqiu_left">
									全球疫情播报
								</view>
								<view class="quanqiu_right">
									截至:****_**_**
								</view>
							</view>
							<view class="fen">
								<view class="trades">
									<view class="textss" :class="currs==0?'actives':''" data-index="0" @tap="sets">
										全国疫情
									</view>
									<view class="textss" :class="currs==1?'actives':''" data-index="1" @tap="sets">
										郑州疫情
									</view>
									<view class="textss" :class="currs==2?'actives':''" data-index="2" @tap="sets">
										海外疫情
									</view>
								</view>
								<swiper  :disable-touch="true" class="swps" style="height: 100vh;" acceleration="false"  :current="currs" @change="sets">
									<swiper-item class="swps_lr">
										<scroll-view class="swps_lr_v">
											<uni-table stripe emptyText="暂无更多数据">
												<uni-tr class="swps_lr_v_t">
													<uni-th class="swps_lr_v_t_t">省份</uni-th>
													<uni-th class="swps_lr_v_t_t">总数</uni-th>
													<uni-th class="swps_lr_v_t_t">治愈人数</uni-th>
													<uni-th class="swps_lr_v_t_t">现有确诊</uni-th>
												</uni-tr>
												<uni-tr>
													<uni-td>河南</uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
												</uni-tr>
												<uni-tr>
													<uni-td>河北</uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
												</uni-tr>
												<uni-tr>
													<uni-td>山东</uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
												</uni-tr>
												<uni-tr>
													<uni-td>安徽</uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
												</uni-tr>
												<uni-tr>
													<uni-td>江苏</uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
												</uni-tr>
												<uni-tr>
													<uni-td>浙江</uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
												</uni-tr>
												<uni-tr>
													<uni-td>山西</uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
												</uni-tr>
												<uni-tr>
													<uni-td>陕西</uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
												</uni-tr>
												<uni-tr>
													<uni-td>内蒙</uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
													<uni-td></uni-td>
												</uni-tr>
											</uni-table>
										</scroll-view>
									</swiper-item>
									<swiper-item class="swps_lr">
										<scroll-view>
											bbb
										</scroll-view> 
									</swiper-item>	
									<swiper-item class="swps_lr">
										<scroll-view>
											ccc
										</scroll-view>
									</swiper-item>
								</swiper>
							</view>
						</view>
					</scroll-view>
				</swiper-item>
				
				<swiper-item>
					<scroll-view>
						<view class="Two_All">
							<view class="Two_All_One">
								<view class="Two_All_One_One">
									出发地
								</view>
								<image class="Two_All_One_img" :src="fenglei1" mode=""></image>
								<view class="Two_All_One_Two">
									目的地
								</view>
							</view>
							<view class="Two_All_Two">
								<view class="Two_All_Two_L">
									出(出发地)
								</view>
								<view class="Two_All_Two_R">
									风险等级
								</view>
							</view>
							<view class="Two_All_Three">
								
							</view>
							<view class="Two_All_Four">
								<view class="Two_All_Four_L">
									入(目的地)
								</view>
								<view class="Two_All_Four_R">
									风险等级
								</view>
							</view>
							<view class="Two_All_Five">
								
							</view>
						</view>
					</scroll-view> 
				</swiper-item>
				
				<swiper-item>
					<scroll-view>
						<view class="Three_All">
							<view class="Three_All_One">
									<image class="Three_All_One_img" :src="fenglei2" mode="">
									</image>
									<text class="Three_All_One_text">
										郑州
									</text>
									<button type="default" class="Three_All_One_button">
										切换城市
									</button>
							</view>
							<view class="Three_All_Two">
								<map class="Three_All_Two_map" :latitude="34.72468" :longitude="113.6401"></map>
							</view>
							<view class="Three_All_Three">
								<uni-table stripe class="Three_All_Three_table" emptyText="暂无更多数据">
									<uni-tr>
										<uni-th>序号</uni-th>
										<uni-th>机构</uni-th>
										<uni-th>位置</uni-th>
									</uni-tr>
									<uni-tr>
										<uni-td>1</uni-td>
										<uni-td>人民医院</uni-td>
										<uni-td>文化路111号</uni-td>
									</uni-tr>
									<uni-tr>
										<uni-td>2</uni-td>
										<uni-td>郑大一附院</uni-td>
										<uni-td>文化路111号</uni-td>
									</uni-tr>
									<uni-tr>
										<uni-td>3</uni-td>
										<uni-td>。。。</uni-td>
										<uni-td>文化路111号</uni-td>
									</uni-tr>
									<uni-tr>
										<uni-td>4</uni-td>
										<uni-td>。。。</uni-td>
										<uni-td>文化路111号</uni-td>
									</uni-tr>
								</uni-table>
							</view>
						</view>
					</scroll-view>
				</swiper-item>
				
				<swiper-item>
					<scroll-view>
						<view class="Three_All">
							<view class="Three_All_One">
									<image class="Three_All_One_img" :src="fenglei1" mode="">
									</image>
									<text class="Three_All_One_text">
										郑州
									</text>
									<button type="default" class="Three_All_One_button">
										切换城市
									</button>
							</view>
							<view class="Three_All_Two">
								<map class="Three_All_Two_map" :latitude="34.72468" :longitude="113.6401"></map>
							</view>
							<view class="Three_All_Three">
								<uni-table stripe class="Three_All_Three_table" emptyText="暂无更多数据">
									<uni-tr>
										<uni-th>序号</uni-th>
										<uni-th>机构</uni-th>
										<uni-th>位置</uni-th>
									</uni-tr>
									<uni-tr>
										<uni-td>1</uni-td>
										<uni-td>aaa小区</uni-td>
										<uni-td>qqq路111号</uni-td>
									</uni-tr>
									<uni-tr>
										<uni-td>2</uni-td>
										<uni-td>bbb小区</uni-td>
										<uni-td>qqq路111号</uni-td>
									</uni-tr>
									<uni-tr>
										<uni-td>3</uni-td>
										<uni-td>。。。</uni-td>
										<uni-td>qqq路111号</uni-td>
									</uni-tr>
									<uni-tr>
										<uni-td>4</uni-td>
										<uni-td>。。。</uni-td>
										<uni-td>qqq路111号</uni-td>
									</uni-tr>
								</uni-table>
							</view>
						</view>
					</scroll-view>
				</swiper-item>	
				
			</swiper>
		</view>
	</view>
</template>

<script>
	import md5 from './md5.js'
	import city from './city.js'
	import citySelect from '@/components/city-select/city-select.vue'
	
	export default {
		data() {
			return {
				appid:15642,
				key:a462db1326b16c12b781830c2eb87adf,
				qq:"请定位",
				iscityshow:false,
				formatName: 'title',
				//当前城市
				activeCity: {
					id: 1,
					title: '南京市'
				},
				//显示的城市数据
				obtainCitys: city,
				istouch:false,
				curr:0,
				currs:0,
				isActive: 0,
				scrollTop: 0,
				id:0,
				covers: [{
					latitude: 34.72468,
					longitude: 113.6401,
				}, {
					latitude: 34.72468,
					longitude: 113.6401,
				}],
				positionInfo: {
					address: '',
					longitude: '', //经度
					latitude: '', //纬度
				},
				fenglei1:"/static/weizhi.png",
				fenglei2:"/static/jiaohuan.png"
				
			}
		},
		components: {citySelect},
		methods: {
			diaoyong(){
				uni.request({
				    url: '/fangyi', //仅为示例，并非真实接口地址。
				    data: {
						appid:this.appid,
						sign:md5('appid' + this.appid + this.key)
				    },
				    header: {
				        'custom-header': 'hello' //自定义请求头信息
				    },
				    success: (res) => {
				        console.log(res.data.result.data);
				    }
				});
			},
			cityClick(item) {
				this.activeCity = item
				this.iscityshow = false
				this.qq = item.title
			},
			showcity(){
				this.iscityshow = true
			},
			touchopen(){
				this.istouch = true
			},
			touchclose(){
				this.istouch = false
			},
			set(e) {
				console.log(e.detail.current)
				let thiss = e.detail.current || e.currentTarget.dataset.index || 0;
				// console.log(thisCurr)
				this.curr = thiss;
			},
			sets(e) {
				console.log(e.detail.current)
				let thisss = e.detail.current || e.currentTarget.dataset.index || 0;
				// console.log(thisCurr)
				this.currs = thisss;
			}
		// 	checked(index) {
		// 		this.isActive = index
		// 	},
		// 	getCurrentLocation() {
		// 		var that = this //在uniapp中药定义一下this才能使用
		// 		uni.getLocation({
		// 			type: 'wgs84',
		// 			success: function(res) {
		// 				console.log(res)
		// 				that.positionInfo.longitude = res.longitude;
		// 				that.positionInfo.latitude = res.latitude;
		// 				that.loAcquire(that.positionInfo.longitude,         
		// 				that.positionInfo.latitude)
		// 			}
		// 		});
		// 	},
		// 	// 获取当前地址
		// 	loAcquire(longitude, latitude) {
		// 		var that = this;
		// 		uni.showLoading({
		// 			title: '加载中',
		// 			mask: true
		// 		});
		// 		var str = `output=jsonp&key='5MTBZ-ZBRRU-AGCV5-BXUUJ-Z5DUV-5OBOQ'=${latitude},${longitude}` 
		// 		this.$jsonp('https://apis.map.qq.com/ws/geocoder/v1/?' + str, {}).then(res => {
		// 			console.log(res);
		// 			uni.hideLoading();
		// 			if (res.status == 0) {
		// 				that.positionInfo.address = '当前位置是:' + res.result.address_component.street_number; //当前定位
		// 			}
		// 		})
		// 	},
		// 	getaddress() {
		// 		var that = this
		// 		uni.chooseLocation({
		// 			success: function(res) {
		// 				that.positionInfo.address = '选择的位置是：' + res.name
		// 			}
		// 		});
		// 	},
		 },
	}
</script>

<style>
	page{
		display: -webkit-box;
		height: 100%;
		width: 100%;
	}

	.Three_All{
		display: flex;
		flex-direction: column;
		width: 90%;
		height: 710px;
		border: 1px solid #797979;
		margin-left: 5%;
	}
	.Two_All_One{
		display: flex;
		flex-direction: row;
		width: 90%;
		height: 50%;
		border: 1px solid red;
	}
	.Three_All_One_img{
		width: 80rpx;
		height: 90rpx;
		margin-left: 30rpx;
	}
	.Three_All_One_text{
		position: absolute;
		margin-top: 20rpx;
		margin-left: 20rpx;
	}
	.Three_All_One_button{
		border: 1px solid #797979;
		/* background-color: #797979; */
		height: 5vh;
		margin-top: -85rpx;
		margin-left: 240rpx;
		width: 31%;
		line-height: 2;
		border-radius: 0;
	}
	.Three_All_Two_map{
		margin-top: 40rpx;
		width: 100%;
		height: 240px;
	}
	.Three_All_Three{
		
	}
	.Three_All_Three_table{
		width: ;
	}



	/* One */
	.One_All{
		border: 1px solid #797979;
		margin: 0 20rpx 0 20rpx;
	}
	.zhengzhou{
		width: 100%;
		display: flex;
		flex-direction: row;
	}
	.img{
		width: 80rpx;
		height: 90rpx;
	}
	.zhengzhou_font{
		position: absolute;
		margin-left: 100rpx;
		margin-top: 20rpx;
	}
	.zhengzhou_botton{
		 border: 1px solid #797979;
		/* background-color: #797979; */
		height: 5vh;
		margin-top: 10rpx;
		margin-left: 150rpx;
		width: 29%;
		line-height: 2;
		border-radius: 0;
	}
	.quanqiu{
		margin-left: 5%;
		width: 90%;
		height: 6vh;
		line-height: 2.5;
		display: flex;
		flex-direction: row;
		margin-top: 25rpx;
		margin-bottom: 25rpx;
		justify-content: space-between;
		border: 1px solid #797979;
		/* background-color: #797979; */
	}
	.quanqiu_left{
		margin-left: 10rpx;
	}
	.quanqiu_right{
		margin-right: 10rpx;
	}
	.fen{
		display: flex;
		flex-direction: column;
		min-height: 100vh;
		width: 100%;
	}
	.trades{
		width: 90%;
		height: 65rpx;
		line-height: 1.7;
		text-align: center;
		color: #000000;
		font-size: 36rpx;
		display: flex;
		flex-direction: row;
		margin-left: 5%;
	}
	.trades view{
		width: 100%;
		float: left;
	}
	.swps{
		margin-top: 20rpx;
		width: 100%;
		height: 100%;
	}
	.swps_lr{
		width: 90%;
		margin-left: 5%;
	}
	.swps_lr_v_t{
		width: 25%;
	}
	.actives {
		position: relative;
		color: #ffffff;
		background-color: #797979;
	}
	.textss{
		border: 1px solid #797979;
		width: 33%;
	}
	.big{
		display: flex;
		flex-direction: column;
		min-height: 100vh;
		width: 100%;
	}
	.trade{
		width: 100%;
		height: 100rpx;
		color: #000000;
		overflow: auto;
		font-size: 36rpx;
		font-family: Alibaba PuHuiTi;
	}
	.trade view{
		text-align: center;
		width: 25%;
		float: left;
	}
	.swp{
		overflow-y: scroll; 
		width: 100%;
		height: 100%;
	}
	.active {
		position: relative;
		color: #1F75FE;
		margin-bottom: 25rpx;
	}

	.content_bobao{
		display: flex;
		flex-direction: column;
		width: 100%;
		justify-content: flex-start;
	}
	
	
	
	
	/* Two */
	.Two_All{
		display: flex;
		flex-direction: column;
	}
	.Two_All_One{
		display: flex;
		flex-direction: row;
		width: 90%;
		height: 80px;
		border: 1px solid #797979;
		margin-left: 5%;
		margin-bottom: 40rpx;
	}
	.Two_All_One_One{
		width: 20%;
		height: 60%;
		border: 1px solid #797979;
		margin-top: 27rpx;
		margin-left: 25rpx;
		text-align: center;
		line-height: 3;
	}
	.Two_All_One_img{
		width: 70px;
		height: 70px;
		margin-left: 100rpx;
	}
	.Two_All_One_Two{
		width: 20%;
		height: 60%;
		border: 1px solid #797979;
		margin-top: 27rpx;
		margin-left: 100rpx;
		text-align: center;
		line-height: 3;
	}
	.Two_All_Two{
		width: 55%;
		height: 38px;
		border: 1px solid #797979;
		margin-left: 5%;
		display: flex;
		flex-direction: row;
	}
	.Two_All_Two_L{
		text-align: center;
		line-height: 2.3;
		margin-right: 135rpx;
	}
	.Two_All_Two_R{
		text-align: center;
		line-height: 2.3;
	}
	.Two_All_Three{
		width: 90%;
		height: 227px;
		border: 1px solid #797979;
		margin-left: 5%;
	}
	.Two_All_Four{
		display: flex;
		flex-direction: row;
		width: 55%;
		height: 38px;
		border: 1px solid #797979;
		margin-left: 5%;
	}
	.Two_All_Four_L{
		text-align: center;
		line-height: 2.3;
		margin-right: 135rpx;
	}
	.Two_All_Four_R{
		text-align: center;
		line-height: 2.3;
	}
	.Two_All_Five{
		width: 90%;
		height: 227px;
		border: 1px solid #797979;
		margin-left: 5%;
	}
</style>
 