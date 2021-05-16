<template>
	<view class="item" @tap="play">
		<image class="icon" :src="icon"></image>
		<view class="content">
			<view class="title">{{ getTitleName(url) }}</view>
			<!-- <view class="detail">{{ detail }}</view> -->
			<view class="icons">
				<view class="icon play">播放：1万+</view>
				<view class="icon share">分享：1000+</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	props: ['title', 'icon', 'detail', 'url'],
	methods: {
		play(url) {
			const title = this.getTitleName(url)
			uni.navigateTo({
				url: `/pages/player/index?name=${title}&url=${this.detail}`
			});
		},
		getTitleName(url){
			const urls = this.detail.split('/')
			 return urls[urls.length -1]
		}
	}
};
</script>

<style lang="less">
.item {
	margin: 12rpx;
	padding-bottom: 20rpx;
	border-bottom: 1rpx solid #cdcdcd;
	box-sizing: border-box;
}

.item::after {
	content: '';
	clear: both;
	display: block;
	width: 0;
	height: 100%;
	visibility: hidden;
}

.icon {
	width: 120rpx;
	height: 120rpx;
	float: left;
	border-radius: 100%;
}

.content {
	padding: 0 20rpx;
	width: calc(100% - 120rpx);
	float: left;
	box-sizing: border-box;
}

.title {
	font-size: 32rpx;
	color: #333333;
}

.detail {
	line-height: 40rpx;
	height: 40rpx;
	font-size: 28rpx;
	color: #999999;
	overflow: hidden;
	text-overflow: ellipsis;
	white-space: nowrap;
}
.icons {
	display: flex;

	.icon {
		flex: 1;
		font-size: 26rpx;
		color: #999999;
		padding-left: 36rpx;
		background-repeat: no-repeat;
		background-position: left center;
		background-size: 30rpx 30rpx;
		height: 40rpx;
		line-height: 40rpx;
		&.play {
			background-image: url(http://47.107.189.64/smallApp/static/play.png);
		}
		&.share {
			background-image: url(http://47.107.189.64/smallApp/static/share.png);
		}
	}
}
</style>
