<template>
	<view class="index-list animated fadeIn slow">
		<view class="index-list1">
			<view class="avatar">
				<image :src="item.userpic" mode="widthFix"></image>
				{{ item.username }}
			</view>
			<view v-show="!isguanzhu" @tap="guanzhu"><view class="icon iconfont icon-zengjia follow">关注</view></view>
		</view>
		<view class="index-list2" @tap="opendetail">{{ item.title }}</view>
		<view class="index-list3" @tap="opendetail">
			<!-- 图片 -->
			<image :src="item.titlepic" mode="widthFix"></image>
			<!-- 视频 -->
			<template v-if="item.type == 'video'">
				<view class="icon iconfont icon-bofang index-list-play"></view>
				<view class="index-list-playinfo">{{ item.playnum }}次播放 {{ item.long }}</view>
			</template>
		</view>
		<view class="index-list4">
			<view class="left">
				<view :class="{ active: infonum.index == 1 }" @tap="caozuo('ding')">
					<view class="icon iconfont icon-icon_xiaolian-mian"></view>
					{{ infonum.dingnum }}
				</view>
				<view :class="{ active: infonum.index == 2 }" @tap="caozuo('cai')">
					<view class="icon iconfont icon-kulian"></view>
					{{ infonum.cainum }}
				</view>
			</view>
			<view class="right">
				<view>
					<view class="icon iconfont icon-pinglun1"></view>
					{{ item.commentnum }}
				</view>
				<view>
					<view class="icon iconfont icon-zhuanfa"></view>
					{{ item.sharenum }}
				</view>
			</view>
		</view>
	</view>
</template>

<script>
export default {
	props: {
		item: Object,
		index: Number
	},
	data() {
		return {
			isguanzhu: this.item.isguanzhu,
			infonum: this.item.infonum
		};
	},
	methods: {
		// 关注
		guanzhu() {
			this.isguanzhu = true;
			uni.showToast({
				title: '关注成功'
			});
		},
		// 顶踩
		caozuo(type) {
			switch (type) {
				case 'ding':
					if (this.infonum.index == 1) {
						return;
					}
					this.infonum.dingnum++;
					if (this.infonum.index == 2) {
						this.infonum.cainum--;
					}
					this.infonum.index = 1;
					break;
				case 'cai':
					if (this.infonum.index == 2) {
						return;
					}
					this.infonum.cainum++;
					if (this.infonum.index == 1) {
						this.infonum.dingnum--;
					}
					this.infonum.index = 2;
					break;
			}
		},
		// 进入详情页
		opendetail() {
			uni.navigateTo({
				url: '../../pages/detail/detail?detailData='+JSON.stringify(this.item)
			});
		}
	}
};
</script>

<style lang="scss">
.index-list {
	padding: 10px;
	border-bottom: 1px solid #eeeeee;
	.index-list1 {
		display: flex;
		align-items: center;
		justify-content: space-between;
		.avatar {
			display: flex;
			align-items: center;
			image {
				width: 84rpx;
				height: 84rpx;
				border-radius: 50%;
				margin-right: 10rpx;
			}
		}
		.follow {
			background: #f4f4f4;
			border-radius: 5upx;
			padding: 0 10upx;
		}
	}
	.index-list2 {
		padding-top: 14rpx;
		font-size: 32rpx;
	}
	.index-list3 {
		padding-top: 14rpx;
		position: relative;
		display: flex;
		justify-content: center;
		align-items: center;
		image {
			width: 100%;
			border-radius: 20rpx;
		}
		.index-list-play {
			position: absolute;
			font-size: 140rpx;
			color: #ffffff;
		}
		.index-list-playinfo {
			position: absolute;
			background: rgba(51, 51, 51, 0.72);
			color: #ffffff;
			bottom: 4px;
			right: 4px;
			border-radius: 20px;
			font-size: 11px;
			padding: 0 6px;
		}
	}
	.index-list4 {
		padding: 14rpx 0;
		display: flex;
		align-items: center;
		justify-content: space-between;
		.left {
			display: flex;
			view {
				margin-right: 10rpx;
				display: flex;
				view {
					margin-right: 10rpx;
				}
			}
			.active {
				color: #c5f61c;
				view {
					color: #c5f61c;
				}
			}
		}
		.right {
			display: flex;
			view {
				display: flex;
				margin-right: 10rpx;
				view {
					margin-right: 10rpx;
				}
			}
		}
	}
}
</style>
