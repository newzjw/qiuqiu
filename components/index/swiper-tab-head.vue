<template>
	<view class="uni-tab-bar">
		<scroll-view scroll-x class="uni-swiper-tab" :style="scrollStyle">
			<block v-for="(tab, index) in tabBars" :key="tab.id">
				<view class="swiper-tab-list" :class="{ active: tabIndex === index }" @tap="tabtap(index)" :style="scrollItemStyle">
					{{ tab.name }} {{ tab.num ? tab.num : '' }}
					<view class="swiper-tab-line"></view>
				</view>
			</block>
		</scroll-view>
	</view>
</template>

<script>
	// 顶部可拖动选项卡
export default {
	props: {
		tabBars: Array,
		tabIndex: Number,
		scrollStyle: {
			type: String,
			default: ''
		},
		scrollItemStyle: {
			type: String,
			default: ''
		}
	},
	data() {
		return {};
	},
	methods:{
		tabtap(index){
			this.$emit('tabtap',index);
		},
	}
};
</script>

<style lang="scss">
.uni-swiper-tab{
	border-bottom: 1rpx solid #EEEEEE;
	.swiper-tab-list{
		color: #969696;
		font-weight: bold;
	}
	.active{
		color: #343434;
		.swiper-tab-line{
			border-bottom: 6rpx solid #FEDE33;
			width: 70rpx;
			margin: auto;
			border-top: 6rpx solid #FEDE33;
			border-radius:20rpx;
		}
	}
}	
</style>
