<template>
	<view>
		<view class="" v-html="con">
			
		</view>
	</view>
</template>

<script>
	export default { 
		data() {
			return {
				key:"98226f8d6b2c89432222edbbc5108336",
				con:"",
				uniquekey:""
			}
		},
		methods: {
			contents(){
				uni.request({
				    url: '/content', //仅为示例，并非真实接口地址。
				    data: {
						key: this.key,
						uniquekey:this.uniquekey
				    },
				    header: {
				        'custom-header': 'hello' //自定义请求头信息
				    },
				    success: (res) => {
						console.log(res.data.result.content);
						if(res.data.error_code==0){
							this.con = res.data.result.content
							uni.setNavigationBarTitle({
								title:res.data.result.detail.title
							})
						}else{
							// alert(res.data.reason)
						}
					}
				});
			}
		},
		onLoad(option) { //option为object类型，会序列化上个页面传递的参数
			console.log(option.uniquekey); //打印出上个页面传递的参数。
			this.uniquekey = option.uniquekey
			this.contents()
		}
	}
</script>

<style>
	
</style>
