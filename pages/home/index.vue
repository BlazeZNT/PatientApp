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
				<text class="title2">{{ stat.title }}</text>
				<view class="icon-container">
				  <image :src="stat.icon" class="icon" />
				</view>
			</div>
			<text class="stat-value">{{ stat.value }}</text>
			<text class="stat-unit">{{ stat.unit }}</text>
		  </view>
		</view>
		
	   <view class="stats-grid">
		  <view class="stat-card" v-for="stat in stats" :key="stat.title">
			<div class="cardtop">
				<text class="title2">{{ stat.title }}</text>
				<view class="icon-container">
				  <image :src="stat.icon" class="icon" />
				</view>
			</div>
			<text class="stat-value">{{ stat.value }}</text>
			<text class="stat-unit">{{ stat.unit }}</text>
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
    title: "Calories\nBurnt",
    value: "1.4k",
	unit: " kCal",
    icon: "/static/fire.png",
  },
  {
    title: "Distance\nCovered",
    value: "3.8",
	unit: " km",
    icon: "/static/run.png",
  },
  {
    title: "Heart\nRate",
    value: "120",
	unit: " bpm",
    icon: "/static/heart.png",
  },
  {
    title: "Sleep\nQuality",
    value: "7.5",
	unit: " hours",
    icon: "/static/bed.png",
  },
  {
    title: "Workout\nSessions",
    value: "10",
	unit: "",
    icon: "/static/squat.png",
  },
  {
    title: "Active\nMinutes",
    value: "120",
	unit: " min",
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
.title2{
	font-size: 17px;
}
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

image {
  width: 40rpx;
  height: 40rpx;
}

.stat-value {
  font-size: 39rpx;
  font-weight: 400;
  color: black;
}
.stat-unit {
  font-size: 15px;
  color: #818898;
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