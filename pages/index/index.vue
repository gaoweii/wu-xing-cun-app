<template>
	<view class="container">
		<!-- 小程序头部兼容 -->
		<!-- #ifdef MP -->
		<!-- <view class="mp-search-box">
			<input class="ser-input" type="text" value="输入关键字搜索" disabled />
		</view> -->
		<!-- #endif -->
		
		<!-- 头部轮播 -->
		<view class="carousel-section">
			<!-- 标题栏和状态栏占位符 -->
			<view class="titleNview-placing"></view>
			<!-- 背景色区域 -->
			<view class="titleNview-background" :style="{backgroundColor:titleNViewBackground}"></view>
			<swiper class="carousel" circular @change="swiperChange">
				<swiper-item v-for="(item, index) in carouselList" :key="index" class="carousel-item" @click="navToDetailPage({title: '轮播广告'})">
					<image :src="item.src" />
				</swiper-item>
			</swiper>
			<!-- 自定义swiper指示器 -->
			<view class="swiper-dots">
				<text class="num">{{swiperCurrent+1}}</text>
				<text class="sign">/</text>
				<text class="num">{{swiperLength}}</text>
			</view>
		</view>
		<!-- 分类 -->	
		<view class="ad-1">
			<image v-bind:src="adSrc" mode="scaleToFill" @click="toPage"></image>
		</view>
		<view class="card">
			<view class="cardPublic card-1 padding-xl radius shadow bg-blue margin-top">
				<svg t="1582086646288" class="cardIcon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1129" width="48" height="48"><path d="M792.73 959.5h-0.06c-33.61-0.02-66.05-14.1-89-38.65-22.95-24.55-34.83-57.87-32.59-91.4l12.55-187.77c0.7-10.48-4.88-20.37-14.22-25.18l-46.17-23.78c-49.53-25.52-70.95-83.64-49.82-135.2l134.44-328.05c0.16-0.39 0.32-0.77 0.49-1.16 17.34-38.76 55.98-63.8 98.45-63.8 59.47 0 107.85 48.38 107.85 107.85v665.23c0 32.58-12.69 63.2-35.73 86.23-23.03 23.01-53.63 35.68-86.19 35.68z m-12.01-799.36L646.57 487.49c-5.46 13.32 0.08 28.34 12.88 34.94l46.16 23.78c37.36 19.25 59.7 58.79 56.9 100.73l-12.55 187.78c-0.8 11.97 3.27 23.38 11.46 32.14s19.3 13.58 31.29 13.59h0.02c11.45 0 22.21-4.45 30.3-12.55 8.1-8.1 12.56-18.86 12.56-30.32V172.35c0-15.88-12.92-28.8-28.79-28.8-11.17 0.01-21.35 6.5-26.08 16.59zM303.99 959.5H303.87c-33.57-0.04-65.97-14.12-88.9-38.65-22.77-24.35-34.64-57.33-32.65-90.59l8.51-289.92c0.69-23.38-8.99-45.66-26.53-61.13a162.298 162.298 0 0 1-54.96-121.71V68.45h79.06V357.5c0 23.87 10.27 46.62 28.18 62.4 35.24 31.06 54.66 75.81 53.28 122.76l-8.53 290.58c-0.01 0.49-0.04 0.98-0.07 1.47-0.8 11.96 3.27 23.38 11.46 32.14 8.17 8.74 19.25 13.56 31.21 13.59 11.96-0.03 23.04-4.85 31.21-13.59 8.19-8.76 12.26-20.17 11.46-32.14-0.03-0.49-0.06-0.98-0.07-1.48L338 542.65c-1.38-46.95 18.04-91.7 53.28-122.76a83.198 83.198 0 0 0 28.18-62.4V68.45h79.06V357.5c0 46.56-20.03 90.92-54.96 121.71-17.55 15.47-27.22 37.75-26.53 61.14l8.51 289.92c2 33.26-9.87 66.24-32.64 90.59-22.88 24.47-55.18 38.54-88.67 38.65-0.09-0.01-0.16-0.01-0.24-0.01z" fill="#ffffff" p-id="1130"></path><path d="M264.4 68.45h79.06V385.7H264.4z" fill="#ffffff" p-id="1131"></path></svg>
				<view class="card-text">附近美食</view>
			</view>
			<view class="card-2 cardPublic padding-xl radius shadow bg-blue margin-top">
				<svg t="1582087610223" class="cardIcon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1436" width="48" height="48"><path d="M930.58 557.04C795.04 518.11 654.22 498.38 512 498.38c-142.22 0-283.05 19.73-418.57 58.66l-28.93 8.31v328.44h79.91V625.87c119.42-31.59 242.93-47.58 367.59-47.58s248.16 15.99 367.59 47.58v267.92h79.91V565.35l-28.92-8.31z" fill="#ffffff" p-id="1437"></path><path d="M212.55 893.87h79.91v-67.09h440.99v67.09h79.91v-147H212.55zM193.96 210.04h639.33v269.25h79.91V130.13H114.05v349.16h79.91z" fill="#ffffff" p-id="1438"></path><path d="M790.15 455.32v-51.05c0-17.62-8.25-50.19-63.49-70.37-28.3-10.34-65.1-16.03-103.63-16.03H400.96c-38.52 0-75.32 5.69-103.62 16.03-55.25 20.18-63.49 52.75-63.49 70.37v51.05h79.91v-41.51c10.89-6.07 40.36-16.04 87.21-16.04h222.07c46.85 0 76.31 9.96 87.21 16.04v41.51h79.9z" fill="#ffffff" p-id="1439"></path></svg>
				<view class="card-text">酒店民宿</view>
			</view>
			<view class="card-3 cardPublic padding-xl radius shadow bg-blue margin-top">
				<svg t="1582087676273" class="cardIcon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1636" width="48" height="48"><path d="M906.73 250.65H774.04L760.24 64.5H480v186.15H335.3l9.36-107.15h57.22v-79H272.26L256 250.65H117.27L77.09 959.5h869.82l-40.18-708.85zM558.99 143.49h127.89l7.94 107.15H558.99V143.49zM191.91 329.64H407.1v550.87h-84.71l6.6-301.97-78.97-1.73-6.64 303.7h-82.69l31.22-550.87zM486.1 880.51V329.64h345.99l31.22 550.87H486.1z" fill="#ffffff" p-id="1637"></path></svg>
				<view class="card-text">本地特产</view>
			</view>
		</view>
		
		<!-- 猜你喜欢 -->
		<view class="f-header m-t">
			<svg t="1582088089483" class="icon" viewBox="0 0 1024 1024" version="1.1" xmlns="http://www.w3.org/2000/svg" p-id="1870" width="40" height="40"><path d="M512.5 920.15l-0.5-0.5-0.49 0.49L143.26 551.9l0.49-0.5-3.65-3.65c-100.8-100.8-100.8-264.82 0-365.62l2.67-2.67C243.58 78.65 407.6 78.65 508.4 179.45l3.6 3.6 3.6-3.6c100.81-100.81 264.82-100.8 365.62 0l2.68 2.68c100.8 100.8 100.8 264.82 0 365.63l-3.6 3.6 0.49 0.49-368.29 368.3z m-0.5-112.63l0.5 0.5 256.17-256.17-0.5-0.49 59.66-59.66c69.89-69.89 69.89-183.6 0-253.49l-2.68-2.68c-69.89-69.89-183.61-69.88-253.49 0L512 295.18l-59.66-59.66c-69.89-69.89-183.6-69.89-253.49 0l-2.67 2.67c-69.9 69.9-69.9 183.61-0.01 253.5l59.61 59.61-0.49 0.5 256.23 256.22 0.48-0.5z" fill="#d81e06" p-id="1871"></path></svg>
			<view class="tit-box">
				<text class="tit">附近</text>
				<text class="tit2">nearby</text>
			</view>
			<text class="yticon icon-you"></text>
		</view>
		
		<view class="guess-section">
			<view 
				v-for="(item, index) in goodsList" :key="index"
				class="guess-item"
				@click="navToDetailPage(item)"
			>
				<view class="image-wrapper">
					<image :src="item.image" mode="aspectFill"></image>
				</view>
				<text class="title clamp">{{item.title}}</text>
				<text class="price">￥{{item.price}}</text>
			</view>
		</view>
		

	</view>
</template>

<script>

	export default {
		

		data() {
			return {
				titleNViewBackground: '',
				swiperCurrent: 0,
				swiperLength: 0,
				carouselList: [],
				goodsList: [],
				adSrc: this.$api.addr + "/index/ad"
			};
		},

		onLoad() {
			this.loadData();
		},
		methods: {
			/**
			 * 请求静态数据只是为了代码不那么乱
			 * 分次请求未作整合
			 */
			/* 手动转化base64为图片太麻烦 */
			/* arrayBufferToBase64: function(buffer) { 
				var binary = "";
				var bytes = new Uint8Array(buffer);
				var len = bytes.byteLength;
				for (var i = 0; i < len; ++i) {
					binary += String.fromCharCode(bytes[i]);
				}
				
			}, */
			
			async loadData() {
				let that = this;
				let carouselList = await this.$api.json('carouselList');
				let goodsList = await this.$api.json('goodsList');
				
				var option = {
					method:"POST",
					url:this.$api.addr + "/index/carouselList",
					data:""
				};
				
				/* 使用封装好的api */
				let res = await this.$api.http(option);
				
				for(var i = 0; i < 3; ++i) {
					let bkColors = res.carousels[i].backgroundColor;
					let image = res.carousels[i].image;
					carouselList[i].background = "rgb("+bkColors.red.toString()+","+bkColors.green.toString()+","+bkColors.blue.toString()+")"
					carouselList[i].src=image;
				}
				
				
				/* 暂时写为这种形式,主要是测试前后端数据的接收问题后期应封装为统一的函数，并且这里还没有针对异步请求做处理 */
				/* uni.request({ 
					url:"http://192.168.0.104:7000/index/carouselList",
					method:"POST",
					success: (res)=> {
						console.log(res.data);
						for(var i = 0; i < 3; ++i) {
							let bkColors = res.data.carousels[i].backgroundColor;
							let image = res.data.carousels[i].image;
							that.carouselList[i].background = "rgb("+bkColors.red.toString()+","+bkColors.green.toString()+","+bkColors.blue.toString()+")"
							that.carouselList[i].src=image;
						}
					}
				}); */
				this.titleNViewBackground = carouselList[0].background;
				this.swiperLength = carouselList.length;
				this.carouselList = carouselList;
				this.goodsList = goodsList || [];
			},
			//轮播图切换修改背景色
			swiperChange(e) {
				const index = e.detail.current;
				this.swiperCurrent = index;
				this.titleNViewBackground = this.carouselList[index].background;
			},
			//详情页
			navToDetailPage(item) {
				//测试数据没有写id，用title代替
				let id = item.title;
				uni.navigateTo({
					url: `/pages/product/product?id=${id}`
				})
			},
			toPage() {
				uni.navigateTo({
					url: "/pages/scenicarea/scenicarea?id=1"
				})
			}
		},
		// #ifndef MP
		// 标题栏input搜索框点击
		onNavigationBarSearchInputClicked: async function(e) {
			this.$api.msg('点击了搜索框');
		},
		//点击导航栏 buttons 时触发
		onNavigationBarButtonTap(e) {
			const index = e.index;
			if (index === 0) {
				this.$api.msg('点击了扫描');
			} else if (index === 1) {
				// #ifdef APP-PLUS
				const pages = getCurrentPages();
				const page = pages[pages.length - 1];
				const currentWebview = page.$getAppWebview();
				currentWebview.hideTitleNViewButtonRedDot({
					index
				});
				// #endif
				uni.navigateTo({
					url: '/pages/notice/notice'
				})
			}
		}
		// #endif
	}
</script>

<style lang="scss">
	/* #ifdef MP */
	.mp-search-box{
		position:absolute;
		left: 0;
		top: 30upx;
		z-index: 9999;
		width: 100%;
		padding: 0 80upx;
		.ser-input{
			flex:1;
			height: 56upx;
			line-height: 56upx;
			text-align: center;
			font-size: 28upx;
			color:$font-color-base;
			border-radius: 20px;
			background: rgba(255,255,255,.6);
		}
	}
	page{
		.cate-section{
			position:relative;
			z-index:5;
			border-radius:16upx 16upx 0 0;
			margin-top:-20upx;
		}
		.carousel-section{
			padding: 0;
			.titleNview-placing {
				padding-top: 0;
				height: 0;
			}
			.carousel{
				.carousel-item{
					padding: 0;
				}
			}
			.swiper-dots{
				left:45upx;
				bottom:40upx;
			}
		}
	}
	/* #endif */
	
	
	page {
		background: #f5f5f5;
	}
	.m-t{
		margin-top: 16upx;
	}
	/* 头部 轮播图 */
	.carousel-section {
		position: relative;
		padding-top: 10px;

		.titleNview-placing {
			height: var(--status-bar-height);
			padding-top: 44px;
			box-sizing: content-box;
		}

		.titleNview-background {
			position: absolute;
			top: 0;
			left: 0;
			width: 100%;
			height: 426upx;
			transition: .4s;
		}
	}
	.carousel {
		width: 100%;
		height: 350upx;

		.carousel-item {
			width: 100%;
			height: 100%;
			padding: 0 28upx;
			overflow: hidden;
		}

		image {
			width: 100%;
			height: 100%;
			border-radius: 10upx;
		}
	}
	.swiper-dots {
		display: flex;
		position: absolute;
		left: 60upx;
		bottom: 15upx;
		width: 72upx;
		height: 36upx;
		background-image: url(data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAMgAAABkCAYAAADDhn8LAAAAGXRFWHRTb2Z0d2FyZQBBZG9iZSBJbWFnZVJlYWR5ccllPAAAAyZpVFh0WE1MOmNvbS5hZG9iZS54bXAAAAAAADw/eHBhY2tldCBiZWdpbj0i77u/IiBpZD0iVzVNME1wQ2VoaUh6cmVTek5UY3prYzlkIj8+IDx4OnhtcG1ldGEgeG1sbnM6eD0iYWRvYmU6bnM6bWV0YS8iIHg6eG1wdGs9IkFkb2JlIFhNUCBDb3JlIDUuNi1jMTMyIDc5LjE1OTI4NCwgMjAxNi8wNC8xOS0xMzoxMzo0MCAgICAgICAgIj4gPHJkZjpSREYgeG1sbnM6cmRmPSJodHRwOi8vd3d3LnczLm9yZy8xOTk5LzAyLzIyLXJkZi1zeW50YXgtbnMjIj4gPHJkZjpEZXNjcmlwdGlvbiByZGY6YWJvdXQ9IiIgeG1sbnM6eG1wTU09Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC9tbS8iIHhtbG5zOnN0UmVmPSJodHRwOi8vbnMuYWRvYmUuY29tL3hhcC8xLjAvc1R5cGUvUmVzb3VyY2VSZWYjIiB4bWxuczp4bXA9Imh0dHA6Ly9ucy5hZG9iZS5jb20veGFwLzEuMC8iIHhtcE1NOkRvY3VtZW50SUQ9InhtcC5kaWQ6OTk4MzlBNjE0NjU1MTFFOUExNjRFQ0I3RTQ0NEExQjMiIHhtcE1NOkluc3RhbmNlSUQ9InhtcC5paWQ6OTk4MzlBNjA0NjU1MTFFOUExNjRFQ0I3RTQ0NEExQjMiIHhtcDpDcmVhdG9yVG9vbD0iQWRvYmUgUGhvdG9zaG9wIENDIDIwMTcgKFdpbmRvd3MpIj4gPHhtcE1NOkRlcml2ZWRGcm9tIHN0UmVmOmluc3RhbmNlSUQ9InhtcC5paWQ6Q0E3RUNERkE0NjExMTFFOTg5NzI4MTM2Rjg0OUQwOEUiIHN0UmVmOmRvY3VtZW50SUQ9InhtcC5kaWQ6Q0E3RUNERkI0NjExMTFFOTg5NzI4MTM2Rjg0OUQwOEUiLz4gPC9yZGY6RGVzY3JpcHRpb24+IDwvcmRmOlJERj4gPC94OnhtcG1ldGE+IDw/eHBhY2tldCBlbmQ9InIiPz4Gh5BPAAACTUlEQVR42uzcQW7jQAwFUdN306l1uWwNww5kqdsmm6/2MwtVCp8CosQtP9vg/2+/gY+DRAMBgqnjIp2PaCxCLLldpPARRIiFj1yBbMV+cHZh9PURRLQNhY8kgWyL/WDtwujjI8hoE8rKLqb5CDJaRMJHokC6yKgSCR9JAukmokIknCQJpLOIrJFwMsBJELFcKHwM9BFkLBMKFxNcBCHlQ+FhoocgpVwwnv0Xn30QBJGMC0QcaBVJiAMiec/dcwKuL4j1QMsVCXFAJE4s4NQA3K/8Y6DzO4g40P7UcmIBJxbEesCKWBDg8wWxHrAiFgT4fEGsB/CwIhYE+AeBAAdPLOcV8HRmWRDAiQVcO7GcV8CLM8uCAE4sQCDAlHcQ7x+ABQEEAggEEAggEEAggEAAgQACASAQQCCAQACBAAIBBAIIBBAIIBBAIABe4e9iAe/xd7EAJxYgEGDeO4j3EODp/cOCAE4sYMyJ5cwCHs4rCwI4sYBxJ5YzC84rCwKcXxArAuthQYDzC2JF0H49LAhwYUGsCFqvx5EF2T07dMaJBetx4cRyaqFtHJ8EIhK0i8OJBQxcECuCVutxJhCRoE0cZwMRyRcFefa/ffZBVPogePihhyCnbBhcfMFFEFM+DD4m+ghSlgmDkwlOgpAl4+BkkJMgZdk4+EgaSCcpVX7bmY9kgXQQU+1TgE0c+QJZUUz1b2T4SBbIKmJW+3iMj2SBVBWz+leVfCQLpIqYbp8b85EskIxyfIOfK5Sf+wiCRJEsllQ+oqEkQfBxmD8BBgA5hVjXyrBNUQAAAABJRU5ErkJggg==);
		background-size: 100% 100%;

		.num {
			width: 36upx;
			height: 36upx;
			border-radius: 50px;
			font-size: 24upx;
			color: #fff;
			text-align: center;
			line-height: 36upx;
		}

		.sign {
			position: absolute;
			top: 0;
			left: 50%;
			line-height: 36upx;
			font-size: 12upx;
			color: #fff;
			transform: translateX(-50%);
		}
	}
	/* 分类 */
	.cate-section {
		display: flex;
		justify-content: space-around;
		align-items: center;
		flex-wrap:wrap;
		padding: 30upx 22upx; 
		background: #fff;
		.cate-item {
			display: flex;
			flex-direction: column;
			align-items: center;
			font-size: $font-sm + 2upx;
			color: $font-color-dark;
		}
		
	}
	.ad-1{
		width: 100%;
		height: 210upx;
		padding: 10upx 0;
		background: #fff;
		image{
			width:100%;
			height: 100%; 
		}
	}
	/* 秒杀专区 */
	.seckill-section{
		padding: 4upx 30upx 24upx;
		background: #fff;
		.s-header{
			display:flex;
			align-items:center;
			height: 92upx;
			line-height: 1;
			.s-img{
				width: 140upx;
				height: 30upx;
			}
			.tip{
				font-size: $font-base;
				color: $font-color-light;
				margin: 0 20upx 0 40upx;
			}
			.timer{
				display:inline-block;
				width: 40upx;
				height: 36upx;
				text-align:center;
				line-height: 36upx;
				margin-right: 14upx;
				font-size: $font-sm+2upx;
				color: #fff;
				border-radius: 2px;
				background: rgba(0,0,0,.8);
			}
			.icon-you{
				font-size: $font-lg;
				color: $font-color-light;
				flex: 1;
				text-align: right;
			}
		}
		.floor-list{
			white-space: nowrap;
		}
		.scoll-wrapper{
			display:flex;
			align-items: flex-start;
		}
		.floor-item{
			width: 150upx;
			margin-right: 20upx;
			font-size: $font-sm+2upx;
			color: $font-color-dark;
			line-height: 1.8;
			image{
				width: 150upx;
				height: 150upx;
				border-radius: 6upx;
			}
			.price{
				color: $uni-color-primary;
			}
		}
	}
	
	.f-header{
		display:flex;
		align-items:center;
		height: 140upx;
		padding: 6upx 30upx 8upx;
		background: #fff;
		image{
			flex-shrink: 0;
			width: 80upx;
			height: 80upx;
			margin-right: 20upx;
		}
		.tit-box{
			flex: 1;
			display: flex;
			flex-direction: column;
		}
		.tit{
			font-size: $font-lg +2upx;
			color: #font-color-dark;
			line-height: 1.3;
		}
		.tit2{
			font-size: $font-sm;
			color: $font-color-light;
		}
		.icon-you{
			font-size: $font-lg +2upx;
			color: $font-color-light;
		}
	}
	
	/* 猜你喜欢 */
	.guess-section{
		display:flex;
		flex-wrap:wrap;
		padding: 0 30upx;
		background: #fff;
		.guess-item{
			display:flex;
			flex-direction: column;
			width: 48%;
			padding-bottom: 40upx;
			&:nth-child(2n+1){
				margin-right: 4%;
			}
		}
		.image-wrapper{
			width: 100%;
			height: 330upx;
			border-radius: 3px;
			overflow: hidden;
			image{
				width: 100%;
				height: 100%;
				opacity: 1;
			}
		}
		.title{
			font-size: $font-lg;
			color: $font-color-dark;
			line-height: 80upx;
		}
		.price{
			font-size: $font-lg;
			color: $uni-color-primary;
			line-height: 1;
		}
	}
	.card{
		padding: 20rpx;
		.card-1{
			background-color: #4399FC;
		}
		
		.card-2{
			background-color: #4CD964;
		}
		
		.card-3{
			background-color: #FA436A;
		}
		
		.cardPublic{
			border-radius: 30rpx;
			margin-top: 60rpx;
			height: 300rpx;
			
		}
		.card-text{
			text-align: center;
			top: 40%;
			font-family: "圆体";
			color: #F5F5F5;
			width: 175rpx;
			height: 30rpx;
			float: right;
			margin-top: 15%;
			margin-right: 30%;
			text-shadow: 1px 1px 2px #F8F6FC;
		}
		.cardIcon{
			position: relative;
			float: left;
			margin-top: 13%;
			margin-left: 30%;
		}
	}

</style>
