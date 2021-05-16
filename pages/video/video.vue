<template>
	<view class="content">
		<video id="myVideo" :src="src" @error="videoErrorCallback" enable-danmu controls  :title="getName(videoList[activeIndex])"></video>
		<view class="list">
			<scroll-view scroll-y="true" show-scrollbar="true" class="srcoll-view">
				<view class="item" v-for="(video, index) in videoList" :key="video.index" v-if="video" @tap="play(video, index)" :class="activeIndex == index ? 'playVideo' : ''">
					{{ getName(video) }}
					<image class="playing" src="http://47.107.189.64/smallApp/static/play.gif" v-if="activeIndex == index"/>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
import videoList from './fileList.js';
export default {
	data() {
		return {
			activeIndex: 0,
			src: videoList[0].src,
			videoList
		};
	},
	onReady: function(res) {
		// #ifndef MP-ALIPAY
		this.videoContext = uni.createVideoContext('myVideo');
		// #endif
	},
	methods: {
		getName(video) {
			const list = video.src.split('/');
			return list[list.length - 1];
		},
		play(video, index) {
			this.activeIndex = index;
			this.src = video.src;
		},
		videoErrorCallback: function(e) {
			uni.showModal({
				content: e.target.errMsg,
				showCancel: false
			});
		}
	}
};
</script>

<style lang="less">
.content {
	position: fixed;
	left: 0;
	right: 0;
	top: 0;
	bottom: 0;
	width: 100%;
	height: 100%;
}
#myVideo {
	width: 100%;
	height: 240px;
}
.list {
	// height: 300px;
	height: calc(100% - 240px);
	padding: 30rpx;
	white-space: nowrap;
	box-sizing: border-box;
	.playVideo {
		color: #f55500;
		.playing{
			width: 40rpx;
			height: 40rpx;
			vertical-align: middle;
			margin-left: 20rpx;
		}
	}
	.srcoll-view {
		height: 100%;
	}
	.item {
		line-height: 60rpx;
		text-align: 20rpx;
	}
}
</style>
