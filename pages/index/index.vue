<template>
	<view>
		<swiper class="screen-swiper" :class="dotStyle ? 'square-dot' : 'round-dot'" :indicator-dots="true" :circular="true" :autoplay="true" interval="5000" duration="500">
			<swiper-item v-for="(item, index) in swiperList" :key="index" class="swiper-item">
				<image :src="item.url" mode="aspectFill" v-if="item.type == 'image'" class="image"></image>
				<video :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover" v-if="item.type == 'video'"></video>
			</swiper-item>
		</swiper>
		<my-section @tap="play(item)" v-for="(item, index) in section" :key="index" :begin="item.begin" :end="item.end"></my-section>
	</view>
</template>

<script>
import { request } from '../../common/request.js';
import { list } from './list.js';
import mySection from './my-section.vue';

export default {
	components: {
		mySection
	},
	data() {
		return {
			swiperList: [
				{
					id: 0,
					type: 'image',
					url: 'http://47.107.189.64/static/img/banner1.jpg'
				},
				{
					id: 1,
					type: 'image',
						url: 'http://47.107.189.64/static/img/banner2.jpg'
				},
				{
					id: 2,
					type: 'image',
						url: 'http://47.107.189.64/static/img/banner3.jpg'
				},
				{
					id: 3,
					type: 'image',
						url: 'http://47.107.189.64/static/img/banner4.jpg'
				},
				{
					id: 4,
					type: 'image',
					url: 'http://47.107.189.64/static/img/banner5.jpg'
				},
				{
					id: 5,
					type: 'image',
					url: 'http://47.107.189.64/static/img/banner6.jpg'
				},
				{
					id: 6,
					type: 'image',
					url: 'http://47.107.189.64/static/img/banner1.jfif'
				},{
					id: 7,
					type: 'image',
					url: 'http://47.107.189.64/static/img/banner2.jfif'
				},{
					id: 8,
					type: 'image',
					url: 'http://47.107.189.64/static/img/banner3.jfif'
				},{
					id: 9,
					type: 'image',
					url: 'http://47.107.189.64/static/img/banner4.jfif'
				},{
					id: 10,
					type: 'image',
					url: 'http://47.107.189.64/static/img/banner5.jfif'
				}
			],
			dotStyle: false,
			page: 0,
			size: 12,
			section: []
		};
	},
	onLoad() {
		this.list = list;
	},
	onReady() {
		this.request();
	},
	onPullDownRefresh() {
		this.page = 0;
		this.list = [];
		this.request();
	},
	onReachBottom() {
		this.request();
	},
	methods: {
		request() {
			uni.showLoading({
				title: '加载中'
			});
			request({
				page: this.page,
				size: this.size,
				success: res => {
					this.list.push(...res);
					this.page++;
					this.section.push({
						begin: this.list.length - res.length,
						end: this.list.length
					});
					uni.stopPullDownRefresh();
					uni.hideLoading();
				}
			});
		}
	}
};
</script>

<style lang="less">
.screen-swiper {
	width: 100%;
	height: 400rpx;
	padding-bottom: 20rpx;
	.swiper-item {
		width: 100%;
		.image {
			width: 100%;
		}
	}
}
</style>
