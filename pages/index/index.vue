<template>
	<view>
		<!-- 自定义导航栏 -->
		<nav-bar>
			<text slot="left" class="font-md ml-3">首页</text>
			<template slot="right">
				<view
					class="flex align-center justify-center bg-icon rounded-circle mr-3"
					style="width: 60rpx; height: 60rpx;"
				>
					<text class="iconfont icon-zengjia"></text>
				</view>
				<view
					class="flex align-center justify-center bg-icon rounded-circle mr-3"
					style="width: 60rpx;height: 60rpx;"
				>
					<text class="iconfont icon-gengduo"></text>
				</view>
			</template>
		</nav-bar>
		<view class="px-3 py-2">
			<view class="position-relative">
				<view class="flex align-center justify-center text-light-muted" style="width: 70rpx;height: 70rpx;position: absolute;top: 0;left: 0;">
					<text class="iconfont icon-sousuo"></text>
				</view>
				<!-- <uni-search-bar :radius="20"  placeholder="搜索网盘文件" @confirm="search" cancelButton="none"></uni-search-bar> -->
				<input style="height: 70rpx;padding-left: 70rpx;" type="text" class="bg-light font-md rounded-circle" placeholder="搜索网盘文件"/>
			</view>
		</view>
	</view>
</template>

<script>
import navBar from '@/components/common/nav-bar.vue';
// import uniSearchBar from '@/components/uni-search-bar/uni-search-bar.vue';
export default {
	components: {
		navBar
		// uniSearchBar
	},
	data() {
		return {
			title: 'Hello'
		};
	},
	onLoad() {},
	methods: {}
};
</script>

<style>
	
</style>