<script>
	export default {
		globalData: {
			statusBarHeight: 0
		},
		onLaunch: function() {
			console.log('App Launch')
			this.globalData.statusBarHeight = uni.getSystemInfoSync().statusBarHeight;

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
	@import './static/font/font.css'; 
	body {
	  font-family: "Figtree";
	  font-weight: 400;
	}
	
	
	view {
		box-sizing: border-box;
	}
	
</style>