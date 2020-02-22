<template>
	<view>
		<view class="cu-card dynamic" :class="isCard?'no-card':''" v-for="(item, index) in content" :key=index>
			<view class="cu-item shadow">
				<view class="cu-list menu-avatar">
					<view class="cu-item">
						<view class="cu-avatar round lg" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10006.jpg);"></view>
						<view class="content flex-sub">
							<view>{{item.name}}</view>
							<view class="text-gray text-sm flex justify-between">
								2019年12月3日
							</view>
						</view>
					</view>
				</view>
				<view class="text-content">
					{{item.text}}
				</view>
				<view class="grid flex-sub padding-lr" :class="isCard?'col-3 grid-square':'col-1'">
					<view class="bg-img" :class="isCard?'':'only-img'" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big10006.jpg);"
					 v-for="(item,index) in isCard?9:1" :key="index">
					</view>
				</view>
				<view class="text-gray text-sm text-right padding">
					<text class="cuIcon-appreciatefill margin-lr-xs"></text>{{item.starsAndComment.stars}}
					<text class="cuIcon-messagefill margin-lr-xs"></text> {{item.starsAndComment.comment}}
				</view>
			</view>
		</view>
		<view class="cu-bar foot input">
			<view class="cu-avatar round" style="background-image:url(https://ossweb-img.qq.com/images/lol/web201310/skin/big91012.jpg);"></view>
			<view class="action">
				<text class="cuIcon-roundaddfill text-grey"></text>
			</view>
			<input @focus="InputFocus" @blur="InputBlur" :adjust-position="false" class="solid-bottom" maxlength="300" cursor-spacing="10"></input>
			<button class="cu-btn bg-green shadow-blur">发送</button>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				isCard: true,
				content: [
					{
						name: "安其拉",
						iconSrc: "",
						date: {
							year: 0,
							month: 0,
							day: 0
						},
						text: "今天天气好好",
						imgSrc: "",
						starsAndComment: {
							stars: 0,
							comment: 0
						}
					},
				],
				publishComment: {
					text: "",
					
				},
				option: {
					method: "POST",
					url: this.$api.addr + "/scenicarea/commentlist?id=1",
					data: {
						id: 1
					}
				}
			};
		},
		methods: {
			IsCard(e) {
				this.isCard = e.detail.value
			},
			async getData() {
				let content = await this.$api.http(this.option);
				this.content = content.comments;
			},
			
		},
		onLoad() {
			this.getData()
		}
	}
</script>

<style>

</style>
