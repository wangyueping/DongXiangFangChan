<template>
	<!-- no message -->
	<view class="content" :style="{height:freeHeight+'px'}" v-if="msgList.length==0">
		<image src="../../static/image/message/nomessage.jpg" mode=""></image>
	</view>
	<!-- no message -->

	<!-- message-list -->
	<view class="container" v-else>
		<tui-swipe-action :actions="actions" @click="handlerButton" v-for="(item,index) in msgList" :key="index" :params="item">
			<block slot="content">
				<tui-list-cell @click="detail" :last="true" :index="item.id">
					<view class="tui-msg-box">
						<image :src="'../../static/image/news/'+item.pic+'.jpg'" class="tui-msg-pic" mode="widthFix"></image>
						<view class="tui-msg-item">
							<view class="tui-msg-name">{{item.nickname}}</view>
							<view class="tui-msg-content">{{item.msg}}</view>
						</view>
					</view>
					<view class="tui-msg-right" :class="[item.level==3?'tui-right-dot':'']">
						<view class="tui-msg-time">{{item.time}}</view>
						<tui-badge type="danger" v-if="item.msgNum>0">{{item.msgNum}}</tui-badge>
					</view>
				</tui-list-cell>
			</block>
		</tui-swipe-action>

	</view>
	<!-- message-list -->

</template>

<script>
	import tuiIcon from "@/components/common/icon/icon.vue";
	import tuiBadge from "@/components/common/badge/badge.vue";
	import tuiListCell from "@/components/common/list-cell/list-cell.vue";
	import tuiSwipeAction from "@/components/common/swipe-action/swipe-action.vue";
	export default {
		components: {
			tuiIcon,
			tuiBadge,
			tuiListCell,
			tuiSwipeAction
		},
		data() {
			return {
				freeHeight: 0,
				// msgList: []
				msgList: [{
					id: 1,
					nickname: "俞广丰",
					pic: "avatar_1",
					msg: "你好，买房吗？",
					msgNum: 2,
					time: "10:22"
				}, {
					id: 2,
					nickname: "俞广丰2号",
					pic: "avatar_2",
					msg: "你好，买房吗？",
					msgNum: 2,
					time: "13:27"
				}, {
					id: 3,
					nickname: "技术交流群",
					pic: "4",
					msg: "[图片]",
					msgNum: 18,
					time: "12:27"
				}, {
					id: 4,
					nickname: "技术交流2群",
					pic: "2",
					msg: "[视频]",
					msgNum: 98,
					time: "10:27"
				}, {
					id: 5,
					nickname: "陈永华",
					pic: "avatar_1",
					msg: "你好，买房吗？",
					msgNum: 2,
					time: "10:27"
				}, {
					id: 6,
					nickname: "尚高旭",
					pic: "avatar_2",
					msg: "你好，买房吗？",
					msgNum: 0,
					time: "10:27"
				}, {
					id: 7,
					nickname: "张新旺",
					pic: "avatar_1",
					msg: "[图片]",
					msgNum: 0,
					time: "10:27"
				}, {
					id: 8,
					nickname: "曾少敏",
					pic: "3",
					msg: "你好，买房吗？",
					msgNum: 0,
					time: "10:27"
				}, {
					id: 9,
					nickname: "波动星球",
					pic: "avatar_1",
					msg: "你好，买房吗？",
					msgNum: 2,
					time: "10:22"
				}, {
					id: 10,
					nickname: "Thorui看点",
					pic: "avatar_2",
					msg: "你好，买房吗？",
					msgNum: 2,
					time: "13:27"
				}],
				actions: [{
					name: '删除',
					color: '#fff',
					fontsize: 30, //单位upx
					width: 80, //单位px
					//icon: 'like.png',//此处为图片地址
					background: '#ed3f14'
				}]
			}
		},
		methods: {
			detail(e) {
				// 消息详情
				let nickName;
				let url = "../message-detail/message-detail"
				for (let i = 0; i < this.msgList.length; i++) {
					if (e.index == this.msgList[i].id) {
						nickName = this.msgList[i].nickname
						this.msgList[i].msgNum = 0 // 清空未读消息数量
						break
					}
				}
				// 拼接url路径地址
				url = url + "?id=" + e.index + "&nickName=" + nickName
				uni.navigateTo({
					url: url
				})
			},
			handlerButton(e) {
				// 子组件传来的时事件对象
				let index = e.index;
				let item = e.item;
				this.operateMsg(index, item)
			},
			operateMsg(index, item) {
				// index:0 删除
				// 删除消息列表中的单条消息
				if (index == 0) {
					for (let i = 0; i < this.msgList.length; i++) {
						if (item.id == this.msgList[i].id) {
							this.msgList.splice(i, 1)
							break
						}
					}
				}
			}
		},
		onShow() {
			uni.getSystemInfo({
				complete: (res) => {
					this.freeHeight = res.windowHeight
				}
			})
		}
	}
</script>

<style>
	/* 消息列表没有消息 */
	.content {
		padding: 0upx 30upx;
		display: flex;
		flex-direction: row;
		justify-content: center;
		align-items: center;
	}

	.content>image {
		width: 400upx;
		height: 500upx;
		margin-top: -40upx;
	}

	/* message-list */
	.tui-msg-box {
		display: flex;
		align-items: center;
	}

	.tui-msg-pic {
		width: 100upx;
		height: 100upx;
		border-radius: 50%;
		display: block;
		margin-right: 24upx;
	}

	.tui-msg-item {
		max-width: 500upx;
		min-height: 80upx;
		overflow: hidden;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
	}

	.tui-msg-name {
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
		font-size: 34upx;
		line-height: 1;
		color: #262b3a;
	}

	.tui-msg-content {
		overflow: hidden;
		white-space: nowrap;
		text-overflow: ellipsis;
		font-size: 28upx;
		line-height: 1;
		color: #9397a4;
	}

	.tui-msg-right {
		max-width: 120upx;
		height: 88upx;
		margin-left: auto;
		text-align: right;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		align-items: flex-end;
	}

	.tui-msg-right.tui-right-dot {
		height: 76upx;
		padding-bottom: 10upx;

	}

	.tui-msg-time {
		width: 100%;
		font-size: 24upx;
		line-height: 24upx;
		color: #9397a4;
	}

	.tui-badge {
		width: auto
	}
</style>
