<template>
  <view class="navigation">
    <view
      v-for="(item, index) in navItems"
      :key="index"
      class="nav-item"
      :class="{ active: activeTab === item.name }"
      @click="navigateTo(item)"
    >
      <view v-if="activeTab === item.name" class="active-bg"></view>
      <image :src="activeTab === item.name ? item.activeIcon : item.icon" class="icon" />
    </view>
  </view>
</template>

<script setup>
import { ref } from "vue";

const activeTab = ref("Home"); // Default active tab

const navItems = [
  { name: "Home", icon: "/static/home.png", activeIcon: "/static/homeactive.png", route: "/pages/home/index" },
  { name: "Search", icon: "/static/discover.png", activeIcon: "/static/search-active.png", route: "/pages/search/index" },
  { name: "Bag", icon: "/static/bell.png", activeIcon: "/static/bellactive.png", route: "/pages/telemedicine/index" },
  { name: "Stats", icon: "/static/chart.png", activeIcon: "/static/stats-active.png", route: "/pages/stats/index" },
  { name: "Profile", icon: "/static/profile.png", activeIcon: "/static/profile-active.png", route: "/pages/profile/index" },
];

const navigateTo = (item) => {
  activeTab.value = item.name;
  uni.redirectTo({
    url: item.route,
  });
};
</script>

<style scoped>
.navigation {
  position: fixed;
  width: 70%; /* Adjust width as needed for central alignment */
  bottom: 20rpx; /* Add a gap between the navigation and the bottom of the page */
  left: 50%; /* Start from the horizontal center */
  transform: translateX(-50%); /* Shift the navigation to align its center */
  height: 100rpx; /* Height of the navigation bar */
  background-color: #17174b; /* Background color */
  border-radius: 50px; /* Rounded corners for the navigation */
  display: flex;
  justify-content: space-around;
  align-items: center;
  box-shadow: 0 4rpx 10rpx rgba(0, 0, 0, 0.2); /* Optional: shadow for a floating effect */
}

.nav-item {
  position: relative; /* Required for placing the active background */
  display: flex;
  justify-content: center;
  align-items: center;
  flex: 1; /* Ensures equal spacing between items */
  text-align: center;
}

.active-bg {
  position: absolute;
  width: 60rpx; /* Larger than the icon */
  height: 60rpx; /* Larger than the icon */
  background-color: #3724eb; /* Background color for active tab */
  border-radius: 50%; /* Circle shape */
  z-index: -1; /* Places it behind the icon */
}

.icon {
  width: 40rpx; /* Size of the icon */
  height: 40rpx; /* Size of the icon */
  z-index: 1; /* Ensure icon appears above the background */
}
</style>