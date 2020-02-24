<template>
	<view class="bkColor">
		<!-- <view>
			<swiper class="swiper" @change="changeText">
				<swiper-item v-for="(item, index) in info.swiperList" :key="index" class="swiper-item">
					<image :src="item.url" mode="aspectFill" class="image"></image>
				</swiper-item>
			</swiper>
			
		</view> -->
		<view class="blank"></view>
		<swiper class="card-swiper swiper" :class="dotStyle?'square-dot':'round-dot'" :indicator-dots="true" :circular="true"
		 :autoplay="true" interval="5000" duration="500" @change="cardSwiper" indicator-color="#8799a3"
		 indicator-active-color="#0081ff">
			<swiper-item v-for="(item,index) in info.swiperList" :key="index" :class="cardCur==index?'cur':''" class="swiper-">
				<view class="swiper-item">
					<image :src="item.url" mode="aspectFill" v-if="item.type=='image'"></image>
					<video :src="item.url" autoplay loop muted :show-play-btn="false" :controls="false" objectFit="cover" v-if="item.type=='video'"></video>
				</view>
			</swiper-item>
		</swiper>
		<view>
			<swiper class="textarea" @transition="changePage">
				<swiper-item>
					<view class="text" v-model="info.introduction">{{info.introduction}}</view>
					
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import bwSwiper from '@/wxcomponents/bw-swiper/bw-swiper.vue'
	
	export default {
		data() {
			return {
				pageChange: false,
				info: {
					swiperList: [{
						id: 0,
						type: "image",
						url: "",
						}
					],
					introduction: "",
					},
				content: "测试数据",	
				options: {
					method: "GET",
					url: this.$api.addr + "/scenicarea",
					data: {
						id: 1
					}
				},
				dotStyle: false,
				towerStart: 0,
				direction: '',
				cardCur: 0
	
			};
		},
		onLoad() {
			this.loadData()
		},
		components:{
			bwSwiper
		},
		methods: {
			changeText: function() { /*当切换轮播图时触发函数, 首先判断是否有多条文本内容,有则改变文本内容,没有就不变 */
				
			},
			DotStyle(e) {
				this.dotStyle = e.detail.value
			},
			cardSwiper(e) {
				this.cardCur = e.detail.current
			},
			
			async loadData() {
				/*通过接口获取图片，文本介绍和评论信息*/
				let info = await this.$api.http(this.options);
				console.log(info);
				this.info = info;
				console.log(this.info)
				
			},
			changePage: function(event) {
				/*在文字发生滑动时触发，切换到评论列表*/
				if(event.detail.dx > 100 && this.pageChange == false) {
					console.log("changepage")
					/* this.pageChange = true; */
					uni.navigateTo({
						url: "comment/comment"
					});
				}
			},
		}
	}
</script>

<style lang="scss">
	.blank{
		background-color: #303133;
		height: 300rpx;
	}
	.bkColor{
		width: 100vw;
		height: 100vh;
		background-color: #303133;
	}
	.swiper{
		height: 65vh;
	}
/* 	.swiper-item{
		
		margin-top: 15vh;
	} */
	.image{
		height: 35vh;
		width: 98vw;
		margin-top: 7vh;
	}
	.textarea{
		height: 25vh;
		/* border-color: #4399FC;
		border-style: solid; */
		.text{
			width: 100vw;
			height: 100vh;
			color: #F5F5F5;
			font-size: 33rpx;
		}
	}

</style>
