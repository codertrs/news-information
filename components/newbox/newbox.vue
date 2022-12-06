<template>
	<view class="newsbox">
		<view class="pic">
			<image :src="item.picurl" mode="aspectFill"></image>
		</view>
		<view class="text">
			<view class="title">
				<view class="con">
					{{item.title}}
				</view>
			</view>
			<view class="info" v-if="!item.looktime">
				<view class="font">{{item.author}}</view>
				<view class="font">{{item.hits}}浏览</view>
			</view>
			<view class="info" v-else>
				<view class="font">浏览时间：{{item.looktime}}</view>
			</view>

		</view>
	</view>
</template>

<script>
	export default {
		name: "newbox",
		props: {
			item: {
				type: Object,
				default: () => ({
					title: "默认标题",
					author: "咸虾米",
					hits: 999,
					picurl: "../../static/images/nopic.jpg",
					looktime: null
				})
			}
		},
		data() {
			return {

			};
		}
	}
</script>

<style lang="scss">
	.newsbox {
		display: flex;
		justify-content: space-between;

		.pic {
			width: 230rpx;
			height: 160rpx;

			image {
				width: 100%;
				height: 100%;
			}
		}

		.text {
			flex: 1;
			padding-left: 20rpx;
			display: flex;
			flex-direction: column;
			justify-content: space-between;

			.title {
				.con {
					font-size: 36rpx;
					color: #333;
					display: -webkit-box;
					overflow: hidden;
					text-overflow: ellipsis;
					-webkit-line-clamp: 2;
					-webkit-box-orient: vertical;
				}
			}

			.info {
				display: flex;
				font-size: 26rpx;
				color: #999;

				.font {
					padding-right: 20rpx;
				}
			}
		}

	}
</style>
