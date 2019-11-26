<template>
	<view class="content">
		<!-- 导航栏 -->
		<nav-bar type="fixed" backState="2000" bgColor="#4BC0EB" fontColor="#FFFFFF">
			<view slot="left" class="nav-bar-left" @tap="chooseCity">
				<text>{{city}}</text>
				<view class="iconfont icon-jiantou"></view>
			</view>

			<view class="nav-bar-middle">
				<view class="search-input" @tap="search">
					<text class="iconfont icon-sousuo"></text>
					<text>请输入关键词搜索</text>
				</view>
			</view>
		</nav-bar>
		<!-- 导航栏 -->

		<!-- 选择城市 -->
		<qu-she-picker ref="showCity" type="city" :dataSet="dataSet" title="选择城市" @hideQSPicker="hideTabBar" @showQSPicker="showTabBar"
		 @confirm="getCity"></qu-she-picker>
		<!-- 选择城市 -->


		<!-- 下拉刷新区域 -->
		<!-- app平台 -->
		<!-- #ifdef APP-PLUS -->
		<mescroll-uni :down="downOption" @down="downCallback" :up="upOption" @up="upCallback" top=142>
			<!-- 轮播图 -->
			<swiper :indicator-dots="true" indicator-active-color="#4BC0EB" :circular="true" :autoplay="true" :interval="3000"
			 :duration="1000" class="banner">
				<swiper-item v-for="imageObj in imageList" :key="imageObj.id">
					<view class="swiper-item">
						<image :src="imageObj.src" mode="widthFix" lazy-load></image>
					</view>
				</swiper-item>
			</swiper>
			<!-- 轮播图 -->

			<!-- 功能板块 -->
			<view class="grid-plate-8">
				<!-- 第一行功能板块 -->
				<view class="grid-plate">
					<block v-for="(gridObj, index) in gridList" :key="index">
						<block v-for="(item, index2) in gridObj.first" :key="index2">
							<view class="plate">
								<view class="iconfont" :class="item.icon"></view>
								<text>{{item.title}}</text>
							</view>
						</block>
					</block>
				</view>
				<!-- 第一行功能板块 -->

				<!-- 第二行功能板块 -->
				<view class="grid-plate">
					<block v-for="(gridObj, index) in gridList" :key="index">
						<block v-for="(item, index2) in gridObj.second" :key="index2">
							<view class="plate">
								<view class="iconfont" :class="item.icon"></view>
								<text>{{item.title}}</text>
							</view>
						</block>
					</block>
				</view>
				<!-- 第二行功能板块 -->
			</view>
			<!-- 功能板块 -->

			<!-- 滚动消息 -->
			<view class="tui-rolling-news">
				<view class="iconfont icon-news"></view>
				<swiper vertical autoplay circular interval="3000" class="tui-swiper">
					<swiper-item v-for="(item,index) in newsList" :key="index" class="tui-swiper-item">
						<view class="tui-news-item" @tap='detail'>{{item}}</view>
					</swiper-item>
				</swiper>
			</view>
			<!-- 滚动消息 -->

			<!-- 热门房源 -->
			<house-list :hotHouseList="hotHouseList">
				<slot>热门房源</slot>
			</house-list>
			<!-- 热门房源 -->
		</mescroll-uni>
		<!-- #endif -->
		<!-- app平台 -->

		<!-- H5平台 -->
		<!-- #ifdef H5 -->
		<mescroll-uni :down="downOption" @down="downCallback" :up="upOption" @up="upCallback" top=102>
			<!-- 轮播图 -->
			<swiper :indicator-dots="true" indicator-active-color="#4BC0EB" :circular="true" :autoplay="true" :interval="3000"
			 :duration="1000" class="banner">
				<swiper-item v-for="imageObj in imageList" :key="imageObj.id">
					<view class="swiper-item">
						<image :src="imageObj.src" mode="widthFix" lazy-load></image>
					</view>
				</swiper-item>
			</swiper>
			<!-- 轮播图 -->

			<!-- 功能板块 -->
			<view class="grid-plate-8">
				<!-- 第一行功能板块 -->
				<view class="grid-plate">
					<block v-for="(gridObj, index) in gridList" :key="index">
						<block v-for="(item, index2) in gridObj.first" :key="index2">
							<view class="plate">
								<view class="iconfont" :class="item.icon"></view>
								<text>{{item.title}}</text>
							</view>
						</block>
					</block>
				</view>
				<!-- 第一行功能板块 -->

				<!-- 第二行功能板块 -->
				<view class="grid-plate">
					<block v-for="(gridObj, index) in gridList" :key="index">
						<block v-for="(item, index2) in gridObj.second" :key="index2">
							<view class="plate">
								<view class="iconfont" :class="item.icon"></view>
								<text>{{item.title}}</text>
							</view>
						</block>
					</block>
				</view>
				<!-- 第二行功能板块 -->
			</view>
			<!-- 功能板块 -->

			<!-- 滚动消息 -->
			<view class="tui-rolling-news">
				<view class="iconfont icon-news"></view>
				<swiper vertical autoplay circular interval="3000" class="tui-swiper">
					<swiper-item v-for="(item,index) in newsList" :key="index" class="tui-swiper-item">
						<view class="tui-news-item" @tap='detail'>{{item}}</view>
					</swiper-item>
				</swiper>
			</view>
			<!-- 滚动消息 -->

			<!-- 热门房源 -->
			<house-list :hotHouseList="hotHouseList">
				<slot>热门房源</slot>
			</house-list>
			<!-- 热门房源 -->
		</mescroll-uni>
		<!-- #endif -->
		<!-- H5平台 -->
		<!-- 下拉刷新区域 -->
	</view>
</template>

<script>
	import navBar from '@/components/index/zhouWei-navBar/index.vue';
	import QuShePicker from '@/components/common/QuShe-picker/QuShe-picker.vue';
	import houseList from '@/components/index/house-list/house-list.vue';
	import mescrollUni from '@/components/common/mescroll-diy/mescroll-meitun.vue';
	export default {
		data() {
			return {
				city: '东乡区',
				dataSet: {
					defaultValue: [13, 9, 1]
				},
				downOption: {
					auto: false
				},
				upOption: {
					auto: false
				},
				imageList: [{
						"id": "1",
						"src": "../../static/image/banner/1.jpg",
						"url": ""
					},
					{
						"id": "2",
						"src": "../../static/image/banner/2.jpg",
						"url": ""
					},
					{
						"id": "3",
						"src": "../../static/image/banner/3.jpg",
						"url": ""
					},
					{
						"id": "4",
						"src": "../../static/image/banner/4.jpg",
						"url": ""
					},
					{
						"id": "5",
						"src": "../../static/image/banner/5.jpg",
						"url": ""
					},
					{
						"id": "6",
						"src": "../../static/image/banner/6.jpg",
						"url": ""
					}
				],
				gridList: [{
						"first": [{
								"icon": "icon-fangchan",
								"title": "新房"
							},
							{
								"icon": "icon-ershoufang",
								"title": "二手房"
							},
							{
								"icon": "icon-zufang",
								"title": "租房"
							},
							{
								"icon": "icon-maifang",
								"title": "卖房"
							}
						]
					},
					{
						"second": [{
								"icon": "icon-ico",
								"title": "房屋估价"
							},
							{
								"icon": "icon-jisuanqi",
								"title": "房贷计算"
							},
							{
								"icon": "icon-VR",
								"title": "VR看房"
							},
							{
								"icon": "icon-bianmin",
								"title": "便民服务"
							}
						]
					}
				],
				newsList: [
					"致力发展负责任的人工智能 中国发布八大治理原则",
					"格兰仕暗示拜访拼多多后遭天猫打压，拼多多高层赞其有勇气",
					"阿里计划将每股普通股拆为8股，增加筹资灵活性"
				],
				hotHouseList: [{
						"image": "../../static/image/banner/1.jpg",
						"title": "北港小学",
						"status": 1, // 1表示在售 2表示售空 3表示即将开售
						"price": "50000",
						"maxArea": 150,
						"minArea": 65,
						"type": 1, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/2.jpg",
						"title": "荆公小学",
						"status": 2, // 1表示在售 2表示售空 3表示即将开售
						"price": "49999",
						"maxArea": 130,
						"minArea": 65,
						"type": 2, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/3.jpg",
						"title": "金水湾",
						"status": 3, // 1表示在售 2表示售空 3表示即将开售
						"price": "29000",
						"maxArea": 160,
						"minArea": 88,
						"type": 3, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/4.jpg",
						"title": "台湾花园",
						"status": 1, // 1表示在售 2表示售空 3表示即将开售
						"price": "33334",
						"maxArea": 150,
						"minArea": 65,
						"type": 3, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/5.jpg",
						"title": "景泰贵族城",
						"status": 2, // 1表示在售 2表示售空 3表示即将开售
						"price": "64449",
						"maxArea": 150,
						"minArea": 65,
						"type": 2, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/6.jpg",
						"title": "碧桂园",
						"status": 1, // 1表示在售 2表示售空 3表示即将开售
						"price": "9999",
						"maxArea": 150,
						"minArea": 65,
						"type": 3, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					}
				]
			}
		},
		components: {
			navBar,
			QuShePicker,
			houseList,
			mescrollUni
		},
		onLoad() {

		},
		methods: {
			// 选择城市
			chooseCity(value) {
				this.$refs.showCity.show()
			},
			// 资讯详情
			detail(e) {
				uni.showToast({
					title: '功能尚未完善~',
					icon: "none"
				})
			},
			// 跳转搜索页面
			search() {
				uni.navigateTo({
					url: "../search/search"
				})
			},
			// 隐藏城市列表选择时同时展示tabbar
			hideTabBar() {
				uni.showTabBar()
			},
			// 显示城市列表选择时同时隐藏tabbar
			showTabBar() {
				uni.hideTabBar()
			},
			// 设置当前城市位置
			getCity(obj) {
				let newCity = obj.data.label
				this.city = newCity.split("-").reverse()[0]
			},
			// 下拉刷新回调函数
			downCallback(mescroll) {
				setTimeout(() => {
					this.hotHouseList.sort(this.shuffle)
					mescroll.endSuccess()
					uni.showToast({
						title: '刷新成功',
						icon: 'none'
					})
				}, 1000)
			},
			// 上拉加载回调函数
			upCallback(mescroll) {
				let curPageData = [{
						"image": "../../static/image/banner/5.jpg",
						"title": "万豪公馆",
						"status": 2, // 1表示在售 2表示售空 3表示即将开售
						"price": "64449",
						"maxArea": 150,
						"minArea": 65,
						"type": 2, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/5.jpg",
						"title": "江南文苑",
						"status": 2, // 1表示在售 2表示售空 3表示即将开售
						"price": "64449",
						"maxArea": 150,
						"minArea": 65,
						"type": 2, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/5.jpg",
						"title": "翰林院",
						"status": 2, // 1表示在售 2表示售空 3表示即将开售
						"price": "64449",
						"maxArea": 150,
						"minArea": 65,
						"type": 2, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/5.jpg",
						"title": "河滨城",
						"status": 2, // 1表示在售 2表示售空 3表示即将开售
						"price": "64449",
						"maxArea": 150,
						"minArea": 65,
						"type": 2, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/5.jpg",
						"title": "鹏泰烟酒",
						"status": 2, // 1表示在售 2表示售空 3表示即将开售
						"price": "64449",
						"maxArea": 150,
						"minArea": 65,
						"type": 2, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/5.jpg",
						"title": "街心花园",
						"status": 2, // 1表示在售 2表示售空 3表示即将开售
						"price": "64449",
						"maxArea": 150,
						"minArea": 65,
						"type": 2, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					},
					{
						"image": "../../static/image/banner/5.jpg",
						"title": "翠碧轩",
						"status": 2, // 1表示在售 2表示售空 3表示即将开售
						"price": "64449",
						"maxArea": 150,
						"minArea": 65,
						"type": 2, // 1表示住宅 2表示别墅 3表示车库
						"city": "东乡",
						"address": "北港小学附近",
						"tags": [
							"新房",
							"二手房",
							"商品房"
						]
					}
				]
				mescroll.optUp.toTop.src = ''
				mescroll.optUp.textNoMore = '--我也是有底线的--'
				let pageNum = mescroll.num; // 页码, 默认从1开始
				let pageSize = mescroll.size; // 页长, 默认每页10条
				setTimeout(() => {
					this.hotHouseList = this.hotHouseList.concat(curPageData); //追加新数据
					mescroll.endBySize(curPageData.length, 13)
				}, 2000)
			},
			// 模拟服务器随机打乱数据
			shuffle(a, b) {
				return Math.random() > .5 ? -1 : 1
			}
		}
	}
</script>

<style>
	.content {
		height: 100%;
	}
	/* 导航栏 */
	.nav-bar-left {
		display: flex;
		flex-direction: row;
		align-items: center;
		margin-left: 30upx;
		font-size: 28upx;
		width: 142upx;
	}

	.nav-bar-left>text {
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}

	.nav-bar-left>view {
		color: #FFFFFF;
		margin-left: 6upx;
		font-size: 24upx;
	}

	.nav-bar-middle {
		width: 100%;
		font-size: 28upx;
	}

	.nav-bar-middle>.search-input {
		width: %100;
		height: 60upx;
		background-color: #F5F5F5;
		border-radius: 30upx;
		border: 1upx solid #FFFFFF;
		text-align: center;
	}

	.nav-bar-middle>.search-input>text {
		color: #A9A9A9;
		font-size: 24upx;
		line-height: 60upx;
	}

	/* 轮播图 */
	.banner {
		height: 300upx;
		width: 100%;
	}

	.banner image {
		width: 100%;
		height: 100%;
	}

	/* 板块宫格 */
	.grid-plate-8 {
		padding: 0upx 30upx;
	}

	.grid-plate {
		display: flex;
		flex-direction: row;
		justify-content: space-around;
	}

	.plate {
		display: flex;
		flex-direction: column;
		align-items: center;
	}

	.plate>view {
		font-size: 60upx;
	}

	/* 滚动消息 */
	.tui-rolling-news {
		width: 85%;
		display: flex;
		align-items: center;
		justify-content: center;
		flex-wrap: nowrap;
		margin: 30upx auto;
		border-radius: 30upx;
		background-color: #F5FCFF;
		padding-left: 15upx;
	}

	.tui-swiper {
		font-size: 28upx;
		height: 50upx;
		flex: 1;
		padding-left: 8upx;
	}

	.tui-swiper-item {
		display: flex;
		align-items: center
	}

	.tui-news-item {
		line-height: 28upx;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
		color: #A9A9A9;
	}

	.icon-news {
		font-size: 28upx;
		color: #56BDE6;
	}
</style>
