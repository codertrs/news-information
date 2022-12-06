<template>
	<view class="index">

		<scroll-view class="navscroll" scroll-x>
			<block v-for="(item,index) in navArr" :key="item.id">
				<view class="row" :class="navIndex===index?'active':''" @click="clickNav(item.id)">
					{{item.classname}}
				</view>
			</block>
		</scroll-view>

		<view class="content">
			<view class="item" v-for="item in listArr">
				<newbox :item="item"></newbox>

			</view>

			<view class="nodata" v-if="!listArr.length">
				<image src="../../static/images/nodata.png" mode=""></image>
				<view class="text">暂无数据</view>
			</view>

		</view>


	</view>
</template>

<script>
	export default {
		data() {
			return {
				navArr: [],
				currentPage: 1,
				navIndex: 0,
				listArr: [],
				loading: 0 //0代表初始化不显示子，1代表加载中，2代表没有更多数据
			}
		},
		onLoad() {
			this.getNav()
			this.getData()
		},
		methods: {
			getNav() {

				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/navlist.php",
					success: (res) => {
						this.navArr = res.data
					}
				})
			},
			getData(classid = 50) {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/newslist.php",
					data: {
						cid: classid,
						page: this.currentPage
					},
					success: (res) => {
						console.log("jinlai")
						console.log("res", res);
						this.listArr = [...this.listArr, ...res.data]
					}
				})
			},
			clickNav(id) {
				let index = this.navArr.findIndex(item => {
					return item.id == id
				})
				this.navIndex = index
				this.currentPage = 1;
				this.listArr = []
				// this.loading=0
			 this.getData(id)
			}
		}
	}
</script>

<style lang="scss" scoped>
	.navscroll {
		height: 100rpx;
		width: 100%;
		background: #F7F8FA;
		position: fixed;
		white-space: nowrap;
		left: 0;
		z-index: 10;
		top: var(--window-top);

		/deep/ ::-webkit-scrollbar {
			width: 4px !important;
			height: 1px !important;
			overflow: auto !important;
			background: transparent !important;
			-webkit-appearance: auto !important;
			display: block;
		}

		.row {
			line-height: 100rpx;
			display: inline-block;
			padding: 10rpx 30rpx;
			font-size: 40rpx;
		}

		.row.active {
			color: #31C27C;
		}
	}

	.content {
		padding: 30rpx;
		padding-top: 130rpx;
		

		.item {
			padding: 20rpx 0;
			border-bottom: 1rpx #e2e2e2 dotted;
		}

		.nodata {
			padding-top: 50rpx;
			display: flex;
			justify-content: center;
			flex-direction: column;
			align-items: center;

			image {
				width: 400rpx;
				height: 400rpx;
			}

			.text {
				color: #999;
				font-size: 20rpx;
			}
		}
	}
</style>
