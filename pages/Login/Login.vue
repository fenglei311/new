
<template>
	<section class="loginContainer" :class="showpage">
		<view class="All_All">
			<view class="All">
				<view class="content" v-for="(item,index) in navList" :key="index" >
					<view :class="{'active':isActive === index}" @click="checked(index)">
						{{item.title}}
					</view>
				</view>
			</view>
			<view class="content_concern content_All" v-if="isActive==0">
				<view :class="{on: loginWay}">
					<section>
						<input type="tel" maxlength="11" placeholder="手机号" v-model="phone" class="login_number ml10">
						<button :disabled="!rightPhone" class="get_verification"
							:class="{right_phone: rightPhone}" @click.prevent="getCode">
							{{computeTime>0 ? `已发送(${computeTime}s)` : '获取验证码'}}
						</button>
					</section>
								
					<section class="login_verification">
						<input type="tel" maxlength="8" placeholder="验证码" v-model="code" class="login_number ml10 mt20">
					</section>
					
					<section class="login_hint">
						温馨提示：未注册帐号的手机号，登录时将自动注册，且代表已同意
						<a href="javascript:;">《用户服务协议》</a>
					</section>
					
				</view>
				<button class="login_submit" @click="goto()">登录</button>
				<a href="javascript:;" class="about_us">关于我们</a>
			</view>
			
			
			<view class="content_time content_All" v-if="isActive==1">
				<section class="login_message">
					<input class="ml10 login_number" type="text" maxlength="11" placeholder="手机/邮箱/用户名" v-model="name">
				</section>
									
				<section class="login_verification">
					<input type="text" maxlength="8" placeholder="密码" v-if="showPwd" v-model="pwd" class="login_number ml10 mt20 pos">
					<input type="password" maxlength="8" placeholder="密码" v-else v-model="pwd" class="login_number ml10 mt20 pos">
					<view class="switch_button" :class="showPwd?'on':'off'" @click="showPwd=!showPwd">
						<view class="switch_circle" :class="{right: showPwd}"></view>
						<span class="switch_text">{{showPwd ? '显示' : '隐藏'}}</span>
					</view>
				</section>
				
				<section class="login_message_two">
					<img class="login_img" src="http://localhost:4000/captcha" alt="captcha"
					@click="getCaptcha" ref="captcha">
					<input type="text" maxlength="11" placeholder="验证码" v-model="captcha" class="login_input_tow">
				</section>
				<button class="login_submit" @click="goto()">登录</button>
				<a href="javascript:;" class="about_us">关于我们</a>
			</view>
		</view>
		
	</section>
</template>

<script>
	import {reqSendCode, reqSmsLogin, reqPwdLogin} from '../../api'
  export default {
    data () {
      return {
		showpage: false,//登录成功为true
        loginWay: false, // true 短信登陆, false 密码
        computeTime: 0, // 计时的时间
        showPwd: false, // 是否显示密码
        phone: '', // 手机号
        code:'', // 短信验证码
        name: '123123', // 用户名
        pwd: '123123', // 密码
        captcha: '', // 图形验证码
        alertText: '', // 提示文本
        alertShow: false, // 是否显示警告框
		isActive: 0,
		navList:[
			{
				index: 0,
				title: '短信登录',
			},{
				index: 1,
				title: "密码登录"
			}
		]
      }
    },

    computed: {
      rightPhone () {
        return /^1\d{10}$/.test(this.phone)
      }
    },

    methods: {
		goto(){
			uni.reLaunch({
			    url: '../center/center?id=0'
			});
		},
		checked(index) {
			this.isActive = index
		},
      // 异步获取短信验证码
      async getCode () {
        // 如果当前没有计时
        if(!this.computeTime) {
          // 启动倒计时
          this.computeTime = 30
          this.intervalId = setInterval(() => {
            this.computeTime--
            if(this.computeTime<=0) {
              // 停止计时
              clearInterval(this.intervalId)
            }
          }, 1000)

          // 发送ajax请求(向指定手机号发送验证码短信)
          const result = await reqSendCode(this.phone)
          if(result.code===1) {
            // 显示提示
            this.showAlert(result.msg)
            // 停止计时
            if(this.computeTime) {
              this.computeTime = 0
              clearInterval(this.intervalId)
              this.intervalId = undefined
            }
          }
        }



      },

      showAlert(alertText) {
        this.alertShow = true
        this.alertText = alertText
      },
      // 异步登陆
      async login () {
        let result
        // 前台表单验证
        if(this.loginWay) {  // 短信登陆
          const {rightPhone, phone, code} = this
          if(!this.rightPhone) {
            // 手机号不正确
            this.showAlert('手机号不正确')
            return
          } else if(!/^\d{6}$/.test(code)) {
            // 验证必须是6位数字
            this.showAlert('验证必须是6位数字')
            return
          }
          // 发送ajax请求短信登陆
          result = await reqSmsLogin(phone, code)

        } else {// 密码登陆
          const {name, pwd, captcha} = this
          if(!this.name) {
            // 用户名必须指定
            this.showAlert('用户名必须指定')
            return
          } else if(!this.pwd) {
            // 密码必须指定
            this.showAlert('密码必须指定')
            return
          } else if(!this.captcha) {
            // 验证码必须指定
            this.showAlert('验证码必须指定')
            return
          }
          // 发送ajax请求密码登陆
          result = await reqPwdLogin({name, pwd, captcha})
        }

        // 停止计时
        if(this.computeTime) {
          this.computeTime = 0
          clearInterval(this.intervalId)
          this.intervalId = undefined
        }

        // 根据结果数据处理
        if(result.code===0) {
          const user = result.data
          // 将user保存到vuex的state
          this.$store.dispatch('recordUser', user)
          // 去个人中心界面
          this.$router.replace('/profile')
        } else {
          // 显示新的图片验证码
          this.getCaptcha()
          // 显示警告提示
          const msg = result.msg
          this.showAlert(msg)
        }
      },
      // 关闭警告框
      closeTip () {
        this.alertShow = false
        this.alertText = ''
      },
      // 获取一个新的图片验证码
      getCaptcha () {
        // 每次指定的src要不一样
        this.$refs.captcha.src = 'http://localhost:4000/captcha?time='+Date.now()
      }
    },

  }
</script>

<style>
	.All_All{
		
	}
	
	
	*{
		padding: 0;
		margin: 0;
	}
	.mt20{
		margin-top: 20px;
	}
	.ml10{
		margin-left: 50px;
		border: 1px solid grey;
		margin-right: 50px;
		border-radius: 5%;
		margin-bottom: 15px;
		height: 30px;
	}
	a{
		text-decoration: none;
	}
/* 	.login_header_title{
		font-size: 40rpx;
		text-align: center;
		margin-top: 15px;
	} */

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
	}
	.content_All{
		margin-top: 40px;
	}
	.login_hint{
		font-size: 14px;
		text-indent: 2em;
	}
	.login_submit{
		margin-top: 20px;
	}
	.swich_button{
		
	}
	.switch_text{
		float: right;
		margin-bottom: 40px;
	}
	.pos{
	}
	.login_input_tow{
		margin-left: 50px;
		border: 1px solid grey;
		margin-right: 50px;
		border-radius: 5%;
		margin-bottom: 15px;
		height: 30px;
		width: 260px;
	}
	.login_img{
		margin-left: 100px;
	}
	.login_message_two{
		
	}
/* 	.login_message{
		border: 1px solid grey;
		margin-left: 50px;
		margin-right: 50px;
		width: 260px;
		height: 30px;
	} */
</style>