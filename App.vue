<script>
	export default {
		globalData: {
			appID: "",
			appSign: "",
			userID: "",
			token: "",
			callID: "",
			isHide: false,
		},
		onLaunch: function () {
			console.log('App Launch')
		},
		onShow: function () {
			console.log('App Show')
			this.globalData.isHide = false
		},
		onHide: function () {
			console.log('App Hide')
			this.globalData.isHide = true
		},
		onError: function (e) {
			console.error(`App Error: ${e.message || e}`, e.stack)
		}
	}
</script>

<style>
</style>
