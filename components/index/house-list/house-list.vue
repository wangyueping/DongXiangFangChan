<template>
	<!-- 热门房源 -->
	<view class="hot-house-list">
		<text>
			<slot></slot>
		</text>
		<block v-for="(hotHouse, index) in hotHouseList" :key="index">
			<view class="hot-house">
				<image :src="hotHouse.image" mode="widthFix" lazy-load></image>
				<view class="hot-house-info">
					<view class="hot-house-title hot-house-info-top">
						<text>{{hotHouse.title}}</text>
						<block v-if="hotHouse.status==1">
							<text>在售</text>
						</block>
						<block v-else-if="hotHouse.status==2">
							<text class="hot-house-empty">售空</text>
						</block>
						<block v-else>
							<text class="hot-house-ready">即将开售</text>
						</block>
					</view>
					<view class="hot-house-price">
						<view>
							<view>
								<text>{{hotHouse.price}}</text>
								<text>元/平起</text>
							</view>
						</view>
						<text>建面{{hotHouse.minArea}}-{{hotHouse.maxArea}}m²</text>
					</view>
					<view class="hot-house-posision">
						<text>
							<block v-if="hotHouse.type==1">住宅</block>
							<block v-else-if="hotHouse.type==2">别墅</block>
							<block v-else>车库</block>
							/{{hotHouse.city}}-{{hotHouse.address}}
						</text>
					</view>
					<view class="hot-house-tags">
						<block v-for="(tag, index) in hotHouse.tags" :key="index">
							<text>{{tag}}</text>
						</block>
					</view>
				</view>
			</view>
		</block>
	</view>
</template>

<script>
	export default {
		props: {
			hotHouseList: {
				type: Array
			}
		},
		data() {
			return {

			}
		},
		methods: {

		}
	}
</script>

<style scoped>
	/* 热门房源 */
	.hot-house-list {
		padding: 0upx 30upx 0upx 30upx;
	}

	.hot-house-list>text {
		font-size: 40upx;
		margin-bottom: 20upx;
	}

	.hot-house-list>.hot-house {
		display: flex;
		flex-direction: row;
		justify-content: flex-start;
		align-items: flex-start;
		margin: 60upx 0upx;

	}

	.hot-house-list>.hot-house:nth-child(2) {
		margin-top: 20upx;
	}

	.hot-house-list>.hot-house:last-child {
		margin-bottom: 20upx;
	}

	.hot-house>image {
		width: 240upx;
		height: 190upx !important;
		border-radius: 10upx;
		flex-shrink: 0;
	}

	.hot-house-info {
		margin-left: 30upx;
		flex-grow: 1;
		margin-top: -12upx;
	}

	.hot-house-title,
	.hot-house-price {
		display: flex;
		flex-direction: row;
	}

	.hot-house-title {
		justify-content: space-between;
		align-items: center;
	}

	.hot-house-title>text:nth-child(1),
	.hot-house-price>view>view,
	.hot-house-posision {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
	}

	.hot-house-title>text:nth-child(1) {
		width: 284upx;
	}

	.hot-house-price>view>view {
		width: 200upx;
	}

	.hot-house-title>text:nth-child(1),
	.hot-house-price>view>view>text:first-child {
		font-size: 32upx;
		font-weight: bold;
	}

	.hot-house-title>text:nth-child(2) {
		background-color: #E0FAF2;
		padding: 0upx 20upx;
		font-size: 24upx;
		color: #13C48E;
	}

	.hot-house-empty {
		color: #dc1010 !important;
		background-color: #fae0e0 !important;
	}

	.hot-house-ready {
		color: #daa110 !important;
		background-color: #f0fcc4 !important;
	}

	.hot-house-price {
		justify-content: flex-start;
		align-items: flex-end;
	}

	.hot-house-price>view {
		color: #F95F35;
	}

	.hot-house-price>text,
	.hot-house-posision>text {
		color: #A5ADAF;
	}

	.hot-house-price>text {
		margin-left: 30upx;
	}

	.hot-house-posision {
		width: 400upx;
	}

	.hot-house-tags>text {
		background-color: #F0F4F5;
		padding: 5upx 10upx;
		font-size: 24upx;
		color: #909D9F;
		border-radius: 10upx;
	}

	.hot-house-tags>text:nth-child(n+2) {
		margin-left: 10upx;
	}
</style>
