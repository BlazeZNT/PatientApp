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
	@import './assets/sfprodisplay/font.css';
	@import './assets/global.css';
	@import './static/font/font.css'; 
	body {
	  font-family: "SF Pro Display", "Segoe UI", Roboto, "Helvetica Neue", Arial, sans-serif;
	  font-size: 16px;
	  font-weight: 400;
	}
	view {
		box-sizing: border-box;
	}
	uni-button:after {
	    content: none !important;
	}
	
</style>