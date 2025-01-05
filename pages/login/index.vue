<template>
	<view class="container">
		<image class="background" src="/static/backgroundimage.png" mode="aspectFill"></image>
		<view class="overlay">
			<text class="title">Let's get started</text>
			<view class="login-buttons">
				<button class="login-button google" @click="loginWithGoogle">
					<image class="icon" src="/static/Google Icon.png" /> 
					<text class="button-text">Login with Google</text>
				</button>
				<button class="login-button apple" @click="loginWithApple">
					<image class="icon" src="/static/Apple Icon.png" /> 
					<text class="button-text">Login with Apple</text>
				</button>
			</view>
		</view>
	</view>
</template>

<script setup>
import { ref, reactive } from "vue";

function loginWithGoogle() {
	uni.navigateTo({
		url: '/pages/login/login'
	})
}

// function loginWithApple() {
// 	slibrary.$router.go("/pages/login/login");
// }
</script>

<style scoped>
.container {
	width: 100%;
	height: 100vh;
	position: relative;
	display: flex;
	justify-content: center;
	align-items: center;
}

.background {
	width: 100%;
	height: 100%;
	position: absolute;
	top: 0;
	left: 0;
	z-index: 1;
}

.overlay {
	width: 100%;
	height: 100%;
	position: absolute;
	top: 0;
	left: 0;
	z-index: 2;
	background-color: rgba(0, 0, 0, 0); /* Optional overlay for better text visibility */
	display: flex;
	flex-direction: column;
	align-items: center;
	justify-content: flex-end;
	padding: 50rpx;
}

.title {
	font-size: 36rpx;
	color: white;
	font-weight: bold;
	margin-bottom: 30rpx;
}

.login-buttons {
	width: 100%;
	display: flex;
	flex-direction: column;
	gap: 20rpx;
	align-items: center;
}

.login-button {
	width: 80%;
	height: 90rpx;
	display: flex;
	align-items: center;
	justify-content: center;
	border-radius: 45rpx;
	font-size: 28rpx;
	font-weight: bold;
	color: black;
	background-color: white;
	box-shadow: 0px 4rpx 8rpx rgba(0, 0, 0, 0.2);
	gap: 10rpx;
}

.google {
	border: 1rpx solid #4285f4;
}

.apple {
	border: 1rpx solid #000;
}

.icon {
	width: 40rpx;
	height: 40rpx;
	margin-right: 10rpx; /* Adds space between the icon and text */
}

.button-text {
	font-size: 28rpx;
	color: black;
	font-weight: bold;
}
</style>