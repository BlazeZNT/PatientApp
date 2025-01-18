<template>
	<view class="page">
		<uv-navbar title="Morning Run" placeholder @leftClick="leftClick"></uv-navbar>
		<lxCalendar />
		<view class="speedBox">
			<view>Average Speed</view>
			<view>7km/h</view>
		</view>
		<view class="cardBox">
			<DataCard title="Calories Burn" data="1.4k" unit="kCal"></DataCard>
			<DataCard title="Distance Covered" data="3.8" unit="km"></DataCard>
		</view>
	</view>
</template>

<script>
	import lxCalendar from '../../components/lx-calendar/lx-calendar.vue'
	import DataCard from '@/components/DataCard.vue'
	export default {
		components: {
			lxCalendar,
			DataCard
		},
		data() {
			return {
			}
		}
	}
</script>

<style lang="scss" scoped>
	.page {
		padding: 32rpx;
		padding-bottom: 150rpx;
	}
	
	.speedBox {
		width: 100%;
		padding: 32rpx;
		background-color: #000;
		margin-top: 32rpx;
		border-radius: 30rpx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		color: #fff;
	}
	
	.cardBox {
		margin-top: 32rpx;
		display: grid;
		grid-template-columns: repeat(2, 1fr);
		grid-gap: 32rpx;
	}

	

	
</style>