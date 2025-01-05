<template>
  <view class="video-call-container">
    <!-- Call Timer -->
    <view class="call-timer">
      <view class="dot"></view>
      <text class="timer-text">06:11</text>
    </view>

    <!-- Mini User Video -->
    <view class="user-video-container">
      <image src="/static/Appointment/patient.png" class="user-video" alt="User's Video" />
    </view>

    <!-- Doctor Information -->
    <view class="doctor-info">
      <text class="doctor-name">Dr. Richardson</text>
      <text class="doctor-specialty">Immunologist</text>
    </view>

    <!-- End Call Button -->
    <view class="end-call-container">
      <button class="end-call-button" @click="endCall">
        <image src="/static/call-end.png" alt="End Call" class="end-call-icon" />
      </button>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue';

const endCall = () => {
  // Implement the logic to end the call
  console.log('Call ended');
};
</script>

<style scoped>
.video-call-container {
  height: 100vh;
  background-image: url('/static/Appointment/doctor.png');
  background-size: cover;
  background-position: center;
  position: relative;
  display: flex;
  flex-direction: column;
  justify-content: flex-end; /* Ensures children align at the bottom */
}

.call-timer {
  position: absolute;
  top: 10px;
  left: 10px;
  display: flex;
  align-items: center;
  background: rgba(0, 0, 0, 0.5);
  padding: 5px 10px;
  border-radius: 20px;
}

.dot {
  width: 10px;
  height: 10px;
  background-color: red;
  border-radius: 50%;
  margin-right: 5px;
}

.timer-text {
  color: white;
  font-size: 14px;
  font-weight: bold;
}

.user-video-container {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 150px;
  height: 150px;
  border-radius: 10px;
  overflow: hidden;
}

.user-video {
  width: 100%;
  height: 100%;
  object-fit: cover;
}

.doctor-info {
  position: absolute;
  bottom: 80px; /* Adjust as needed to place above the end button */
  left: 20px;
  background: rgba(0, 0, 0, 0.6); /* Slightly darker background for contrast */
  padding: 10px 15px;
  border-radius: 10px;
  display: flex;
  flex-direction: column;
}

.doctor-name {
  color: white;
  font-size: 18px;
  font-weight: bold;
}

.doctor-specialty {
  color: white;
  font-size: 14px;
}

.end-call-container {
  display: flex;
  justify-content: center;
  padding: 20px;
}

.end-call-button {
  background-color: red;
  border: none;
  border-radius: 50%;
  padding: 15px;
  display: flex;
  justify-content: center;
  align-items: center;
  cursor: pointer;
}

.end-call-icon {
  width: 30px;
  height: 30px;
}
</style>