<template>
  <view class="container">
    <!-- Success Icon -->
    

    <!-- Success Message -->
    <view class="success-message">
		<view class="success-icon-container">
		  <image src="/static/success-icon.png" class="success-icon" />
		</view>
      <text class="title">Successfully Set Your Goals</text>
      <text class="subtitle">
        You've successfully set your health and fitness goals! Get ready to transform your life with a personalized plan tailored just for you.
      </text>
    </view>

    <!-- Goals Summary -->
    <view class="goals-summary">
      <view v-for="goal in goals" :key="goal.title" class="goal-item">
        <view class="icon-container">
          <image :src="goal.icon" class="icon" />
        </view>
        <view class="goal-info">
          <text class="goal-title">{{ goal.title }}</text>
          <text class="goal-value">{{ goal.value }}</text>
        </view>
      </view>
    </view>

    <!-- Start Now Button -->
    <view class="start-now-container">
      <button class="start-now-button" @click="startNow">Start Now</button>
    </view>
  </view>
</template>

<script setup>
import button from "@/components/button/index.vue"

// Goals data
const goals = [
  {
    icon: "/static/shoe.png",
    title: "Daily Step Count",
    value: "10,000 Steps",
  },
  {
    icon: "/static/squat.png",
    title: "Weekly Workout",
    value: "6 Sessions",
  },
  {
    icon: "/static/plate.png",
    title: "Calorie Intake",
    value: "1,200 Calories",
  },
  {
    icon: "/static/water.png",
    title: "Water Daily",
    value: "2,200 Liters",
  },
  {
    icon: "/static/bed.png",
    title: "Sleep Hours",
    value: "7 Hours",
  },
];

// Start Now button action
const startNow = () => {
	uni.navigateTo({
		url: '/pages/home/index'
	})
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: space-between;
  height: 100vh;
  background-color: #ffffff;
  padding: 20rpx;
}

.success-icon-container {
  margin-top: 50rpx;
  margin-bottom: 50rpx;
}

.success-icon {
  width: 100rpx;
  height: 100rpx;
}

.success-message {
  display: flex;
  flex-direction: column;
  text-align: center;
  margin-top: 30rpx;
}

.title {
  font-size: 36rpx;
  font-weight: bold;
  color: #2b1a88;
  margin-bottom: 15rpx;
}

.subtitle {
  font-size: 28rpx;
  color: #8c8c8c;
  line-height: 40rpx;
}

.goals-summary {
  width: 90%;
  background-color: transparent;
  border-radius: 20rpx;
  padding: 30rpx;
  margin-top: 30rpx;
  border: 1px solid rgba(129, 136, 152, 0.3); /* Feint border */
  box-shadow: 0 0 5rpx rgba(129, 136, 152, 0.2); /* Optional soft shadow */
}

.goal-item {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 25rpx;
}

.goal-item:last-child {
  margin-bottom: 0; /* Remove margin from the last child */
}

.goal-icon image {
  width: 50rpx;
  height: 50rpx;
}

.goal-info {
  display: flex;
  flex: 1;
  justify-content: space-between;
  align-items: center;
  margin-left: 20rpx;
}

.goal-title {
  font-size: 28rpx; /* Larger font for title */
  color: black;
}

.goal-value {
  font-size: 28rpx;
  color: #818898;
}

.start-now-container {
  margin-top: 50rpx;
  width: 100%;
}

.start-now-button {
  display: flex;
  width: 80%;
  height: 2.8125rem;
  background-color: #3724eb;
  color: #ffffff;
  font-size: 0.875rem;
  font-weight: bold;
  border-radius: 1.40625rem;
  justify-content: center;
  align-items: center;
}

.icon-container {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f2f3f5; /* Very light grey */
  width: 80rpx; /* Adjust the size to make it circular */
  height: 80rpx; /* Keep height equal to width for a perfect circle */
  border-radius: 50%; /* Makes it a circle */
}

.icon {
  width: 50rpx; /* Adjust the icon size */
  height: 50rpx;
}
</style>