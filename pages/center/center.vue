<template>
	<view>
		<view class="center">
			<view class="center_man">
				<view class="center_man_img">
					
				</view>
				<view class="center_man_name">
					{{login > 1 ? '请登录' : '风雷'}}
				</view>
			</view>
			<view class="line">
				
			</view>
			<view class="center_collect">
				我的收藏
			</view>
			<view class="line">
				
			</view>
			<view class="center_history">
				浏览历史
			</view>
			<view class="line">
				
			</view>
			<view class="center_settings">
				应用设置
			</view>
			<view class="center_exit" @click="goto(login)">
				{{login > 1 ? '登录' : '退出登录'}}
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				login:2,
				name:"风雷", 
				name1:"退出登录"
			}
		},
		methods: {
			goto(){
				var that = this;
				that.login = 0;
				uni.reLaunch({
				    url: '../Login/Login'
				});
			},
		},
 		onLoad(option) { 
 			console.log(option.id);
			this.login = option.id;
		},
	}
</script>

<style>
	.line{
		margin: 10px 0px 10px 0px;
		border: 1px solid lightgrey;
	}
	.center{
		display: flex;
		flex-direction: column;
	}
	.center_man{
		display: flex;
		flex-direction: row;
		margin-top: 25px;
		margin-left: 20px;
	}
	.center_man_img{
		width: 100px;
		height: 100px;
		border-radius: 100%;
		background: url(../../static/my-select.png) no-repeat center lightgrey;
	}
	.center_man_name{
		font-size: 24px;
		margin-left: 50px;
		margin-top: 30px;
	}
	.center_collect{
		width: 100%;
		height: 100px;
		line-height: 80px;
		/* border: 1px solid red; */
	}
	.center_history{
		width: 100%;
		height: 100px;
		line-height: 80px;
		/* border: 1px solid red; */
	}
	.center_settings{
		width: 100%;
		height: 70px;
		text-align: center;
		line-height: 70px;
		border: 1px solid grey;
	}
	.center_exit{
		width: 100%;
		height: 70px;
		margin-top: 20px;
		text-align: center;
		line-height: 70px;
		border: 1px solid grey;
		color: red;
	}
</style>