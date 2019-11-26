<template>
	<view>
		<hx-navbar :back="false" :fixed="true" right-icon="scan" :background-color="[[28, 187, 180],[141, 198, 63]]">
			<block slot="left">
				<view class="city">
					<view>新疆</view>
					<uni-icons type="arrowdown" color="#333333" size="22" />
				</view>
			</block>
			<view class="input-view">
				<uni-icons type="search" size="22" color="#666666" />
				<input confirm-type="search" class="input" type="text" placeholder="输入搜索关键词" @confirm="confirm">
			</view>
		</hx-navbar>
	</view>
</template>

<script>
	import uniIcons from '../../components/common/uni-icons/uni-icons.vue';
	import hxNavbar from '../../components/common/hx-navbar/hx-navbar';
	export default {
		data() {
			return {

			}
		},
		components: {
			hxNavbar,
			uniIcons
		},
		methods: {

		}
	}
</script>

<style>
	.city {
		display: flex;
		flex-direction: row;
		align-items: center;
		justify-content: center;
		width: 100%;
		margin-left: 8px;
		white-space: nowrap;
	}
</style>
