<template>
	<view>
		<!-- 未登录的模板 -->
		<template v-if="!islogin">
			<view class="u-f-ajc">登陆球球，体验更多功能</view>
			<!-- 第三方登陆 -->
			<other-login></other-login>
			<!-- 账号密码登陆 -->
			<view class="u-f-ajc" @tap="openLogin">
				账号密码登陆
				<view class="icon iconfont icon-jinru"></view>
			</view>
		</template>
		<!-- 登录后的模板 -->
		<template v-else>
			<!-- 登陆 -->
			<home-info :homeinfo="homeinfo"></home-info>
		</template>
		<!-- 数据 -->
		<home-data :homedata="homedata"></home-data>
		<!-- 广告位 -->
		<view class="home-adv u-f-ajc animated fadeIn fast" >
			<image src="../../static/demo/demo20.jpg" mode="widthFix" lazy-load></image>
		</view>
		<!-- 功能列表 -->
		<view class="home-list">
			<block v-for="(item,index) in list" :key="index">
				<home-list-item :item="item" :index="index"></home-list-item>
			</block>
		</view>
	</view>
</template>

<script>
import otherLogin from '../../components/home/other-login.vue';
import homeInfo from "../../components/home/home-info.vue";
import homeData from "../../components/home/home-data.vue";
import homeListItem from "../../components/home/home-list-item.vue";
export default {
	components: {
		otherLogin,
		homeInfo,
		homeData,
		homeListItem
	},
	data() {
		return {
			islogin: false,
			homeinfo:{
				userpic:"../../static/demo/userpic/11.jpg",
				username:"昵称",
				totalnum:0,
				todaynum:0,
			},
			homedata:[
				{ name:"糗事", num:0 },
				{ name:"动态", num:0 },
				{ name:"评论", num:0 },
				{ name:"收藏", num:0 },
			],
			list:[
				{ icon:"liulan",name:"浏览历史",clicktype:"",url:""},
				{ icon:"huiyuanvip",name:"球球认证",clicktype:"",url:"" },
				{ icon:"keyboard",name:"审核球球",clicktype:"",url:"" },
			]
		};
	},
	// 跳转到用户设置
	onNavigationBarButtonTap(e) {
		if(e.index===0){
			uni.navigateTo({
				url: '../user-set/user-set',
			});
		}
	},
	methods:{
		openLogin(){
			console.log('123')
			uni.navigateTo({
				url: '../login/login'
			});
		}
	}
};
</script>

<style></style>
