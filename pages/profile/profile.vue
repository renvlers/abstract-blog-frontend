<template>
	<view :class="{ 'dark-theme': darkTheme }">
		<!--登陆后内容-->
		<view class="global-view" v-if="isLogin">
			<view class="u-m-t-20">
			</view>
			<view class="container u-flex user-box u-p-l-30 u-p-r-20 u-p-b-30">
				<view class="u-m-r-10 u-padding-top-25">
					<u-avatar :src="user.u_avatar_url" size="140"></u-avatar>
				</view>
				<view class="u-flex-1">
					<view class="u-font-18 u-p-b-20 u-margin-top-25 u-margin-left-8 ">{{user.u_nickname}}</view>
					<!--插值表示法-->
					<view class="u-font-14 u-margin-top-15 u-margin-left-8 u-tips-color ">uid:{{user.u_id}}</view>
				</view>
				<view class="u-m-l-10 u-p-10">
					<u-icon name="arrow-right" color="#969799" size="28" @click="mySelf()"></u-icon>
				</view>
			</view>
			<view class="container u-m-t-20">
				<u-cell-group style="border-radius: 10rpx;">
					<u-cell-item icon="edit-pen" :arrow="false">
						<view class="u-font-14 u-margin-top-15 u-margin-left-40 u-tips-color">
							<u-input v-model="user.u_signature" :customStyle="inputStyle" :placeholder="`${translations.编辑个签}, ${translations.展示我的独特态度}`"
								@click="topersonality()">
							</u-input>
						</view>
					</u-cell-item>
					<u-cell-item icon="home" :title="translations.我的主页" @click="myCollection()"></u-cell-item>
					<u-cell-item icon="heart" :title="translations.我的关注" @click="myFollowing()"></u-cell-item>
					<u-cell-item icon="account" :title="translations.我的粉丝" @click="myFans()"></u-cell-item>
					<u-cell-item icon="chat" :title="translations.智能聊天" @click="smartChat()"></u-cell-item>
					<u-cell-item icon="setting" :title="translations.设置" @click="set"></u-cell-item>
					<u-cell-item icon="more-dot-fill" :title="translations.关于" @click="about()"></u-cell-item>
					
				</u-cell-group>
			</view>
			<view class="container">
				<u-button class="exit" type="error" @click="exit()">{{translations.退出}}</u-button>
			</view>
		</view>
		<!--未登陆时内容-->
		<view class="global-view" v-else>
			<view class="container">
				<u-navbar :is-back="false" title="　" :border-bottom="false">
					<view class="u-flex u-row-right" style="width: 100%;">
						<view class="camera u-flex u-row-center">
							<u-icon name="camera-fill" color="#000000" size="48"></u-icon>
						</view>
					</view>
				</u-navbar>
				<view class="u-flex user-box u-p-l-30 u-p-r-20 u-p-b-30">
					<view class="u-m-r-10">
						<u-avatar src="pic" size="140"></u-avatar>
					</view>
					<view class="u-flex-1">
						<view class="u-font-18 u-p-b-20">未登录</view>
						<view class="u-font-14 u-tips-color">u_id:</view>
					</view>
					<view class="u-m-l-10 u-p-10">
						<u-icon name="arrow-right" color="#969799" size="28"></u-icon>
					</view>
				</view>
			</view>

			<view class="container"><u-button class="btn" type="primary" @click="toLogin()">登录</u-button></view>
		</view>
	</view>
</template>

<script>
	import Chinese from '@/languages/zh-CN'
	import English from '@/languages/en-US'
	export default {
		data() {
			return {
				show: true,
				isLogin: false,
				inputStyle: {
					fontSize: '16px'
				},
				translations: this.language === "en-US" ? English : Chinese
			}
		},
		onLoad(){
			uni.setNavigationBarTitle({
				title: this.translations.我的
			});
			uni.setTabBarItem({
				index: 0,
				text: this.translations.首页
			});
			uni.setTabBarItem({
				index: 1,
				text: this.translations.分类
			});
			uni.setTabBarItem({
				index: 2,
				text: this.translations.投稿
			});
			uni.setTabBarItem({
				index: 3,
				text: this.translations.动态
			});
			uni.setTabBarItem({
				index: 4,
				text: this.translations.我的
			});
		},
		onShow() { //在页面显示的时候调用这个周期函数
			//1.从storage中读取用户信息
			let user = uni.getStorageSync("user")
			//user = {id": 2,name:""......}
			//2.判断用户信息是否为空，为空说明用户未登录
			if (user) { //如果用户信息存在，显示个人中心页面
				this.isLogin = true
				this.user = user
			}
			Î
			if (this.darkTheme) {
				uni.setNavigationBarColor({
					frontColor: '#ffffff', // 这是文字颜色，设置为白色
					backgroundColor: '#2a2a2a', // 这是背景颜色，设置为深色
				});
			} else {
				uni.setNavigationBarColor({
					frontColor: '#000000',
					backgroundColor: '#f8f8f8'
				});
			}
		},
		methods: {
			myFollowing() {
				uni.navigateTo({
					url: "/pages/myfollow/myfollow"
				});
			},
			myFans() {
				uni.navigateTo({
					url: "/pages/myfans/myfans"
				});
			},
			toLogin: function() {
				uni.navigateTo({
					url: '/pages/login/login'
				})
			},
			//退出登录的函数
			exit: function() {
				//清空storage中的数据
				uni.clearStorageSync("user")
				//刷新当前页面
				uni.reLaunch({
					url: '/pages/profile/profile'
				})
			},
			mySelf: function() {
				uni.navigateTo({
					url: '/pages/user/mySelf/mySelf'
				})
			},
			about: function() {
				uni.navigateTo({
					url: '/pages/about/about'
				})
			},
			set: function() {
				uni.navigateTo({
					url: '/pages/set/set'
				})
			},
			topersonality: function() {
				uni.navigateTo({
					url: '/pages/user/personality/personality'
				})
			},
			myarticles: function() {
				uni.navigateTo({
					url: '/pages/articles/articles'
				})
			},
			myCollection: function() {
				uni.navigateTo({
					url: '/pages/myhome/myhome'
				})
			},
			smartChat() {
				uni.navigateTo({
					url: '/pages/spark/spark'
				});
			}

		}
	}
</script>

<style lang="scss">
	.exit {
		width: 100%;
	}

	.btn {
		width: 100%;
	}
</style>