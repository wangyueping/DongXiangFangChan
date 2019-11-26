<script>
	export default {
		onLaunch: function() {
			console.log('App Launch')
		},
		onShow: function() {
			console.log('App Show')
		},
		onHide: function() {
			console.log('App Hide')
		}
	}
</script>

<style>
	/*每个页面公共css */
	/* 自定义css样式 */
	@import url("./common/css/common.css");
	/* uni官方css样式 */
	@import url("./common/css/uni.css");
	/* 阿里字体css样式 */
	@import url("./common/css/iconfont.css");
	/* animate.css */
	@import url("./common/css/animate.css");
</style>
