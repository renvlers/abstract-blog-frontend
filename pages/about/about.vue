<template>
	<view class="global-view" :class="{ 'dark-theme': darkTheme }">
		<view class="container">
		<u-image width="100%" border-radius="5" height="400rpx" :src="src"></u-image>
		<view class="u-m-t-20">
			<u-cell-group>
				<u-cell-item :title="translations.当前版本" value="V 1.0":arrow="false"></u-cell-item>
				<u-cell-item :title="translations.版本更新" :value="translations.已是最新版本":arrow="false"></u-cell-item>
				<u-cell-item :title="translations.功能介绍"></u-cell-item>
				<u-cell-item :title="translations.帮助"></u-cell-item>
				<u-cell-item :title="translations.反馈"></u-cell-item>
			</u-cell-group>
		</view>
	</view>
	</view>
</template>

<script>
	import Card from '@/pages/card/card'
	import Chinese from '@/languages/zh-CN'
	import English from '@/languages/en-US'
	export default {
		components: {
		  Card
		},
		onLoad(){
			uni.setNavigationBarTitle({
				title: this.translations.关于
			})
		},
		data() {
			return {			
				src:'https://ts3.cn.mm.bing.net/th?id=OIP-C._tHrVEicLiuuAFW_zLGzfQHaEf&w=321&h=194&c=8&rs=1&qlt=90&o=6&dpr=1.3&pid=3.1&rm=2',
				translations: this.language === "en-US" ? English : Chinese
			}
		},
		methods: {
			
			
		}
	}
</script>

<style scoped lang="scss">
	.wrap {
			padding: 24rpx;
		}
	
		.u-row {
			margin: 40rpx 0;
		}
	
		.demo-layout {
			height: 80rpx;
			border-radius: 8rpx;
		}
	
		.bg-purple {
			background: #d3dce6;
		}
	
		.bg-purple-light {
			background: #e5e9f2;
		}
	
		.bg-purple-dark {
			background: #99a9bf;
		}

</style>
