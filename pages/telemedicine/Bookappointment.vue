<template>
  <view class="appointment-page">
    <!-- Header Section -->
    <view class="header">
      <view class="header-left">
        <image src="/static/back-arrow.png" class="back-arrow" @click="goBack" />
      </view>
      <text class="title">Book Appointment</text>
      <view class="header-right">
        <image src="/static/bell.png" class="bell-icon" />
      </view>
    </view>

    <!-- Tabs -->
    <view class="tab-container">
        <button
          class="tab-button"
          :class="{ active: activeTab === 'My Appointment' }"
          @click="setActiveTab('My Appointment')"
        >
          My Appointment
        </button>
        <button
          class="tab-button"
          :class="{ active: activeTab === 'Consult Now' }"
          @click="setActiveTab('Consult Now')"
        >
          Consult Now
        </button>
        <button
          class="tab-button"
          :class="{ active: activeTab === 'History' }"
          @click="setActiveTab('History')"
        >
          History
        </button>
      </view>

    <!-- Appointment List -->
    <view class="appointment-list">
      <view
        v-for="(appointment, index) in appointments"
        :key="index"
        class="appointment-card"
      >
        <view class="card-content">
          <image :src="appointment.image" class="doctor-image" />
          <view class="appointment-info">
            <text class="doctor-name">{{ appointment.name }}</text>
            <text class="doctor-specialty">{{ appointment.specialty }}</text>
            <text v-if="appointment.status === 'HAPPEN NOW'" class="appointment-status">
              HAPPEN NOW
            </text>
            <text v-else class="appointment-time">
              {{ appointment.date }} • {{ appointment.time }}
            </text>
          </view>
          <view class="appointment-actions">
            <button class="consult-button">Consult Now</button>
          </view>
        </view>
        <!-- Reschedule and Cancel Buttons -->
        <view
          v-if="appointment.status !== 'HAPPEN NOW'"
          class="extra-actions"
        >
			<button class="reschedule-action">Reschedule</button>
			<view class="divider"></view>
			<button class="cancel-action">Cancel</button>
        </view>
      </view>
    </view>
	<view class="footer">
	    <mybutton text="Book An Appointment" class="appointment-button" />
	    <view class="icon-container">
	      <image src="/static/vector.png" class="bell-icon" />
	    </view>
	  </view>

  </view>
</template>

<script setup>
import { ref } from "vue";
import mybutton from "@/components/button/index.vue"

const activeTab = ref("My Appointment");

const appointments = [
  {
    image: "/static/doctor2.png",
    name: "Dr. Richardson",
    specialty: "Immunologist",
    status: "HAPPEN NOW",
    date: "",
    time: "",
  },
  {
    image: "/static/doctor2.png",
    name: "Dr. Richard Lee",
    specialty: "Cardiologist",
    status: "Upcoming",
    date: "07/12/2024",
    time: "10:00 am",
  },
];

const goBack = () => {
  console.log("Go Back to Previous Page");
};

const setActiveTab = (tab) => {
  activeTab.value = tab;
};
</script>

<style scoped>
.appointment-page {
  background-color: #f5f5f5;
  height: 100vh;
  display: flex;
  flex-direction: column;
}

.header {
  display: flex;
  align-items: center; /* Vertically center items */
  justify-content: space-between; /* Distribute space between items */
  padding: 20rpx;
  padding-top: 30px;
  background-color: white;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
  position: relative; /* Optional: For fine-tuning child positions */
}

.header-left,
.header-right {
  display: flex;
  align-items: center;
}

.title {
  flex: 1; /* Let the title take available space */
  text-align: center; /* Center the title text */
  font-size: 36rpx;
  font-weight: bold;
  color: black;
}

.back-arrow {
  width: 30rpx;
  height: 30rpx;
}

.bell-icon {
  width: 40rpx;
  height: 40rpx;
}

.tab-container {
  display: flex;
  background-color: #f9f9f9; /* Light background for the tab container */
  border-radius: 40px; /* Slightly smaller rounded container */
  padding: 3px; /* Reduce padding around the container */
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1); /* Subtle shadow */
  margin: 20px auto; /* Center the tab container */
  width: auto; /* Auto-adjust width to fit content */
  width: 80%; /* Restrict maximum width */
}

.tab-button {
  flex-grow: 0; /* Prevent buttons from stretching unnecessarily */
  flex-shrink: 0; /* Prevent buttons from shrinking too much */
  flex-basis: auto; /* Allow buttons to size based on their content */
  background-color: transparent; /* Default transparent background */
  color: #000000; /* Default text color */
  font-size: 12px; /* Smaller font size */
  font-weight: bold; /* Bold text */
  border: none; /* Remove border */
  outline: none; /* Remove outline on focus */
  text-align: center; /* Center text */
  cursor: pointer; /* Pointer cursor */
  border-radius: 40px; /* Make buttons rounded */
  padding: 6px 12px; /* Reduced padding for smaller buttons */
  transition: background-color 0.2s ease, transform 0.2s ease; /* Smooth hover effect */
}

.tab-button.active {
  background-color: #0034ee; /* Blue background for active tab */
  color: #ffffff; /* White text for active tab */
  transform: scale(0.95); /* Slightly smaller active button size */
}

.appointment-list {
  flex: 1;
  padding: 20rpx;
}

.appointment-card {
  background-color: white;
  border-radius: 10rpx;
  margin-bottom: 20rpx;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

.card-content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 30rpx; /* Padding only applies to the main card content */
}

.doctor-image {
  width: 100rpx;
  height: 100rpx;
  border-radius: 5rpx;
  margin-right: 20rpx;
}

.appointment-info {
  flex: 1;
  display: flex;
  flex-direction: column;
}

.doctor-name {
  font-size: 28rpx;
  font-weight: bold;
  color: black;
}

.doctor-specialty {
  font-size: 24rpx;
  color: #888888;
  margin-top: 5rpx;
}

.appointment-status {
  font-size: 22rpx;
  color: #10c469;
  margin-top: 5rpx;
}

.appointment-time {
  font-size: 22rpx;
  color: #888888;
  margin-top: 5rpx;
}

.appointment-actions {
  display: flex;
  align-items: center;
}

.consult-button {
  background-color: #0034ee;
  color: white;
  padding: 10rpx 20rpx;
  border-radius: 50rpx;
  font-size: 22rpx;
  border: none;
  cursor: pointer;
}

.extra-actions {
  display: flex;
  justify-content: space-between;
  padding: 10rpx 20rpx; /* Padding for the actions */
  background-color: #f9f9f9;
  border-radius: 0 0 10rpx 10rpx; /* Rounded corners only for the bottom */
  border-top: 1rpx solid #e0e0e0; /* Add a subtle border between card and actions */
}

uni-button:after {
    content: none !important;
}

.reschedule-action,
.cancel-action {
  font-size: 22rpx;
  align-items: center;
  cursor: pointer;
  width: 100%;
  border: none; /* Remove border */
  outline: none; /* Remove outline on focus */
  text-align: center; /* Center align the text */
  padding: 0; /* Optional: Remove padding for a cleaner look */
}

.reschedule-action {
  color: #0034ee;
  
}

.cancel-action {
  color: #ff4d4d;
}

.divider {
  width: 1rpx; /* Thickness of the divider */
  height: auto; /* Allow the height to adjust based on parent container */
  align-self: stretch; /* Ensure it spans the full height of the container */
  background-color: #e0e0e0; /* Light gray color for the divider */
  margin: 0 10rpx; /* Add horizontal spacing around the divider */
}

.footer {
  display: flex;
  justify-content: space-between; /* Space between the button and the icon */
  align-items: center;
  padding: 20rpx;
  background-color: #f5f5f5; /* Optional background color */
  margin-bottom: 30rpx;
}

.appointment-button {
  flex: 1; /* Allow the button to take available space */
  margin-right: 10rpx; /* Add space between the button and the icon */
}

.icon-container {
  display: flex;
  margin-left: 30rpx;
  justify-content: center;
  align-items: center;
  width: 100rpx;
  height: 100rpx;
  background-color: white; /* Circle background color */
  border-radius: 50%; /* Make it circular */
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1); /* Optional shadow */
}
</style>