<template>
	<view class="page">
		<uv-navbar title="Insight" placeholder @leftClick="leftClick"></uv-navbar>
		<view class="card">
			<YourDailyGoals />
		</view>
		<view class="card">
			<Sleep></Sleep>
		</view>
		<view class="card">
			<Period></Period>
		</view>
		<view class="card">
			<HeartRate></HeartRate>
		</view>
		<view class="card">
			<Hydration></Hydration>
		</view>
		<view class="card">
			<YourWeeklyTarget></YourWeeklyTarget>
		</view>
	</view>
</template>

<script>
	import lxCalendar from '../../components/lx-calendar/lx-calendar.vue'
	import DataCard from '@/components/DataCard.vue'
	import YourDailyGoals from '@/components/insightCard/YourDailyGoals.vue'
	import Sleep from '@/components/insightCard/Sleep.vue'
	import Period from '@/components/insightCard/Period.vue'
	import HeartRate from '@/components/insightCard/HeartRate.vue'
	import Hydration from '@/components/insightCard/Hydration.vue'
	import YourWeeklyTarget from '@/components/insightCard/YourWeeklyTarget.vue'
	
	export default {
		components: {
			lxCalendar,
			DataCard,
			YourDailyGoals,
			Sleep,
			Period,
			HeartRate,
			Hydration,
			YourWeeklyTarget
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
	
	.card {
		margin-bottom: 32rpx;
	}
	

	
</style>