<template>
	<view class="home">
		<view class="entry video" @tap="entry('/pages/video/video')"><view class="circle">视频播放</view></view>
		<view class="entry mp3" @tap="entry('/pages/index/index')"><view class="circle">音频播放</view></view>
	</view>
</template>

<script>
export default {
	data() {
		return {};
	},
	methods: {
		entry(path) {
			uni.navigateTo({
				url: path
			});
		}
	}
};
</script>

<style lang="less">
.home {
	.entry {
		width: 94%;
		margin: 30rpx auto;
		height: 400rpx;
		background-size: auto 120%;
		background-position: center;
		background-repeat: no-repeat;
		position: relative;
		background-color: #eeebe6;
		.circle {
			width: 180rpx;
			height: 180rpx;
			border-radius: 50%;
			background-color: rgba(0, 0, 0, 0.3);
			text-align: center;
			line-height: 180rpx;
			position: absolute;
			left: 50%;
			top: 50%;
			transform: translate(-50%, -50%);
			font-size: 32rpx;
			font-weight: 600;
			color: #ffffff;
		}
		&.video {
			background-image: url(http://47.107.189.64/smallApp/static/bg1.png);
		}
		&.mp3 {
			background-image: url(http://47.107.189.64/smallApp/static/bg2.png);
		}
	}
}
</style>
