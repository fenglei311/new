##新闻资讯App搭建过程说明

### 首页编写（index.vue）
	-观察原型图，发现首页分为上中下三部分
	-创建上中下三个view容器，头部菜单栏，中间轮播图，底部新闻列表
	
#### 头部菜单栏
    -使用了scroll-view组件，实现菜单栏的横向滚动
	-使用了flex布局，实现了菜单栏每一项横向布局
	-使用了css样式 write-spice: nowrap; 实现了菜单栏每一项强制在同一行显示
	-使用了css样式 margin-top: 25rpx; 实现了菜单栏文字居中
	-使用了css样式 last-child选择器以及css样式 padding-right:30rpx; 实现了菜单栏最后一项距离右边框30rpx
	-使用了选择器 ::-webkit-scrollbar,隐藏了scroll-view的滚动条
	-使用css样式 position: fixde; 将菜单栏始终固定到了顶部
#### 工具标签
	-由于头部菜单栏设置为绝对定位，导致轮播图被头部菜单栏遮挡了一部分
	-我们在头部菜单栏和中间轮播图之间添加了一个view作为工具标签
	-将工具标签的width和height设置为头部菜单栏的width和height
	-将工具标签的position属性设置成相对定位。（默认就是相对定位）
#### 中间轮播图
    -使用了swiper标签和swiper-item标签，组成轮播图样式
	-使用了circular属性，让轮播图保持衔接滑动
	-使用了autoplay属性，让轮播图保持自动播放
	-使用了interval="3000"，定义轮播图每隔3000毫秒播放一次
	-使用了indicator-dots属性，定义轮播图显示面板指示点
#### 底部新闻列表
	-使用flex布局搭建新闻列表整体样式
	-使用image组件加载新闻列表中图片
	-使用text组件进行文字加载


###首页逻辑编写

####头部菜单栏逻辑编写
	-使用v-for循环绑定了titleList数据，将菜单栏中每一项标签循环出来
	-使用三元运算符， :class="index==isActive?'active':''" ,以及事件 :@click="updateType(item.key,index)" ,实现了菜单栏切换更改相应菜单样式
####中间轮播图逻辑编写
	-在data中信件了bannerList数组，将轮播图数据录入进去
	-使用v-for指令将轮播图中每一项标签绑定到bannerList数组上
####底部新闻标签逻辑编写
	-在data中信件了newsList数组，将新闻列表数据录入进去
	-使用v-for指令将新闻列表中每一项标签绑定到newsList数组上
####数据请求
	-使用uni.request()方法进行数据请求 //进入uni-app官网，点击头部菜单栏API选项，点击左侧菜单栏，网络，发起请求，uni.request，找到相应的代码，复制粘贴，并进行修改
	-跨域问题解决方案：
		*浏览器访问不同域名（IP）下的资源，会出现跨域问题
		*我们在本地启动一个node.js服务，浏览器访问node.js服务不会出现跨域
		*node.js服务访问远程服务器资源，不会出现跨域
		*所以我们将node.js服务作为中间代利，帮助我们请求远程数据

###其他功能

####下拉刷新
	-使用生命周期函数onPullDownRefresh()实现下拉刷新功能
		*需要在pages.json中找到首页对应的style，设置"enablePullDownRefresh": true
		*当用户啊进行下拉刷新时，onPullDownRefresh()中请求信的数据代码块就会执行
		*我们需要在请求数据代码的complete回调函数中，设置关闭下拉刷新动作，即：uni.stoPullDownRefresh()
	-使用生命周期函数onReachBottom()实现了滚动条到达底部时，加载下一页数据
		*当用户将页面滚动条滑到底部时，onReachBottom()中请求下一页的数据代码块就会执行
	-点击不同菜单，加载不同数据
		*使用@click绑定菜单栏点击事件方法：updateType(newsType,newIndex)
		*在undateType()方法中这是type的值，重新请求数据
		*使用uni.pageScrollTo()将页面滚动条设置到顶部
####新闻详情（content.vue)
	-在index页面中使用@click绑定了goto()方法
	-使用uni-navigateTo()跳转到新闻详情页，并将新闻ID传递了过去
	-在新闻详情页onLoad()生命周期函数中，接收了新闻ID，并赋值给uniquekey
	-并调用了requestNewsContent()请求到了新闻请求数据（注意跨域问题）
	-使用了v-html指令将带有标签的数据加载到了页面上
	-在数据请求成功的回调函数中，使用了uni.setNavigationBarTitle()设置了头部标题为新闻标题