<template>
	<view class="bkColor">
		<view>
			<swiper class="swiper" @change="changeText">
				<swiper-item v-for="(item, index) in info.imgSrcs" :key="index" class="swiper-item">
					<image :src="item" mode="aspectFill" class="image"></image>
				</swiper-item>
			</swiper>
			
		</view>
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
					imgSrcs: [
						"",
						"",
						""
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
			
			async loadData() {
				/*通过接口获取图片，文本介绍和评论信息*/
				let info = await this.$api.http(this.options);
				console.log(info);
				for(var i = 0; i < 3; ++i) {
					this.info.imgSrcs[i] = info.imgSrcs[i];
				}
				this.info.introduction = info.introduction;
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
	.bkColor{
		width: 100vw;
		height: 100vh;
		background-color: #303133;
	}
	.swiper{
		height: 65vh;
		
	}
	.swiper-item{
		
		margin-top: 15vh;
	}
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
