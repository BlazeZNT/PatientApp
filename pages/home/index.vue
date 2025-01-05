<template>
	<scroll-view class="scroll-container" scroll-y="true">
	  <view class="container">
		<!-- Header Section -->
		<view class="header">
		  <text class="title">Summary</text>
		  <view class="tab-buttons">
			<button
			  class="tab-button"
			  :class="{ active: activeTab === 'Fitness' }"
			  @click="setActiveTab('Fitness')"
			>
			  FITNESS
			</button>
			<button
			  class="tab-button"
			  :class="{ active: activeTab === 'Nutrition' }"
			  @click="setActiveTab('Nutrition')"
			>
			  NUTRITION
			</button>
		  </view>
		</view>

		<!-- Daily Average Section -->
		<view class="daily-average">
		  <text class="daily-title">Daily Average</text>
		  <div class="Btmline">
			  <text class="daily-value">5,093 </text>
			  <span class="daily-unit">STEPS</span>
		  </div>
		  
		  <image src="/static/graph.png" class="graph-image" />
		</view>

		<!-- Statistics Section -->
	   <view class="stats-grid">
		  <view class="stat-card" v-for="stat in stats" :key="stat.title">
			<div class="cardtop">
				<text class="stat-title">{{ stat.title }}</text>
				<view class="icon">
				  <image :src="stat.icon" />
				</view>
			</div>
			<text class="stat-value">{{ stat.value }}</text>
		  </view>
		</view>
		
		<view class="stats-grid">
		  <view class="stat-card" v-for="stat in stats" :key="stat.title">
			<div class="cardtop">
				<text class="stat-title">{{ stat.title }}</text>
				<view class="icon">
				  <image :src="stat.icon" />
				</view>
			</div>
			<text class="stat-value">{{ stat.value }}</text>
		  </view>
		</view>

		<!-- Bottom Navigation -->
		<NavigationComponent />
	  </view>
	</scroll-view>
</template>

<script setup>
import { ref } from "vue";
import * as echarts from "echarts";
import NavigationComponent from "/components/navigation/index.vue"

const activeTab = ref("Fitness");

// Stats data
const stats = [
  {
    title: "Calories Burnt",
    value: "1.4k kCal",
    icon: "/static/fire.png",
  },
  {
    title: "Distance Covered",
    value: "3.8 km",
    icon: "/static/run.png",
  },
  {
    title: "Heart Rate",
    value: "120 bpm",
    icon: "/static/heart.png",
  },
  {
    title: "Sleep Quality",
    value: "7.5 hours",
    icon: "/static/bed.png",
  },
  {
    title: "Workout Sessions",
    value: "10",
    icon: "/static/squat.png",
  },
  {
    title: "Active Minutes",
    value: "120 min",
    icon: "/static/walk.png",
  },
];

// Navigation items
const navItems = [
  { title: "Home", icon: "/src/static/home.png", active: true },
  { title: "Activities", icon: "/static/squat.png", active: false },
  { title: "Nutrition", icon: "/static/squat.png", active: false },
  { title: "Progress", icon: "/static/squat.png", active: false },
  { title: "Profile", icon: "/static/squat.png", active: false },
];

// Handle tab switch
const setActiveTab = (tab) => {
  activeTab.value = tab;
};
</script>

<style scoped>
	
.container {
  display: flex;
  flex-direction: column;
  background-color: #ffffff;
  min-height: 100vh;
}

.header {
  background-color: #2b1a88;
  padding: 20rpx;
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: left;
}

.title {
  margin-top: 60rpx;
  font-size: 36rpx;
  color: white;
  font-weight: bold;
  margin-bottom: 20rpx;
  text-align: left;
  
}

.tab-buttons {
  display: flex;
  width: 50%;
  justify-content: center; /* Optional: centers the buttons */
  align-items: center;
  background-color: #17174b;
  border-radius: 5px;
  padding: 5px; /* Padding around the buttons for spacing */
}

.tab-button {
  background-color: transparent; /* Transparent background for inactive buttons */
  border-radius: 5px; /* Rounded corners */
  font-size: 12px; /* Font size remains consistent */
  color: white;
  text-align: center;
  cursor: pointer;

  
}

.tab-button.active {
  background-color: #3724eb; /* Background for the active tab */
  color: white; /* Active tab text color */
  transform: scale(0.9); /* Scale down the size of the active button */
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.2); /* Optional: Add shadow for better emphasis */

}

.daily-average {
  padding: 20rpx;
  text-align: left;
  background-color: #2b1a88;
  color: white;
}

.daily-title {
  font-size: 28rpx;
  color: #b3b3b3;
}
.Btmline{
	margin-top: 10px;
}
.daily-value {
  font-size: 48rpx;
  font-weight: bold;
}

.daily-unit {
  font-size: 24rpx;
}

.graph-image {
  height:14vh;
  margin-top: 10px;
  width: 100%;
  margin-bottom: 20px;
}

.stats-grid {
  display: grid;
  grid-template-columns: repeat(2, 1fr);
  gap: 30rpx;
  padding: 20rpx;
  background-color: #f9f9f9;
  margin-top: 30rpx;
}
.cardtop{
	display: flex;
	justify-content: space-between;
	margin-bottom: 20px;
}
.stat-card {
  background-color: white;
  border-radius: 10rpx;
  padding: 20rpx;
  box-shadow: 0 2rpx 5rpx rgba(0, 0, 0, 0.1);
}

.icon image {
  width: 40rpx;
  height: 40rpx;
}

.stat-title {
  margin-top: 10rpx;
  margin-bottom: 20rpx;
  font-size: 24rpx;
  color: #2b1a88;
}

.stat-value {
  font-size: 28rpx;
  font-weight: bold;
  color: #2b1a88;
}

</style>