<template>
	<view class="content">
		<view class="header">
		  <view class="header-left">
			<image src="/static/arrow-left.png" class="back-arrow" @click="goBack"/>
		  </view>
		  <text class="title">Doctor Details</text>
		  <view class="header-right">
			<image src="/static/bell.png" class="bell-icon" />
		  </view>
		</view>
		<view class="containerbox">
			<!-- Doctor Info Section -->
				<view class="doctor-info">
				  <image src="/static/doctor2.png" class="doctor-image" />
				  <text class="live-badge">LIVE</text>
				  <text class="doctor-name">Dr. Richardson</text>
				  <view class="doctor-rating">
					<text class="doctor-specialty">Immunologist</text>
					<text class="rating">★ 4.5</text>
				  </view>
				</view>
			
				<!-- Health Complaints Section -->
				<view class="form-group">
				  <text class="label">Tell your health complaints</text>
				  <textarea
					class="textarea"
					placeholder="Describe your health complaints..."
					v-model="formData.complaints"
				  ></textarea>
				</view>
			
				<view class="medical-record">
				  <!-- Heart Rate Card -->
				  <view class="record-card">
				    <view class="heartcard">
				      <text class="record-label">Heart Rate</text>
				      <image src="/static/appointment/heartbeat.png" alt="heart" class="icon" />
				    </view>
				    <text class="record-value">120 <text class="unit">bpm</text></text>
				  </view>
				
				  <!-- Add Others Card -->
				  <view class="add-card">
				    <image src="/static/appointment/heartbeat.png" alt="add" class="add-icon" />
				    <text class="add-label">Add others</text>
				  </view>
				</view>
			
				<!-- Select Date Section -->
				<view class="select-date">
				  <text class="label">Select Date</text>
				  <view class="calendar">
					<!-- Calendar grid will be added here -->
					<customcal/>
				  </view>
				</view>
			
				<!-- Select Time Section -->
				  <view class="select-time">
				    <text class="label">Select Time</text>
				    <view class="time-slots">
				      <button
				        v-for="(time, index) in timeSlots"
				        :key="index"
				        :class="['time-slot', { selected: time === selectedTime }]"
				        @click="selectTime(time)"
				      >
				        {{ time }}
				      </button>
				    </view>
				  </view>
		</view>
		<view class="footer">
			<mybutton text="Book An Appointment" class="appointment-button" @click="handleNextClick" />
		</view>

    </view>
</template>

<script setup>
import { reactive } from "vue";
import { ref } from 'vue';
import mybutton from "@/components/button/index.vue"
import customcal from "@/components/customCalendar/index.vue"



const formData = reactive({
  complaints: "",
});

const days = [7, 14, 21, 28];
const timeSlots = ["08:00", "10:00", "14:00", "16:00"];
const selectedDay = reactive({ value: 7 });
const selectedTime = ref('08:00');

const selectDay = (day) => {
  selectedDay.value = day;
};

const selectTime = (time) => {
  console.log("hello")
  selectedTime.value = time;
};

const handleNextClick = () => {
	uni.navigateTo({
		url: '/pages/telemedicine/completeAppointment'
	})
}
</script>

<style scoped>
.content {
  min-height: 100vh; /* Ensures content takes the full viewport height */
  display: flex; /* Use Flexbox for layout */
  flex-direction: column; /* Arrange children in a column */
  background-color: #f5f5f5;
}

.footer {
  margin-top: auto; /* Pushes footer to the bottom */
  padding: 10px;
  text-align: center; /* Center-align content */
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
  margin-bottom: 20rpx;
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

.containerbox{
	padding: 30rpx;
}

.doctor-info {
  display: flex;
  flex-direction: column;
  align-items: center;
  margin-bottom: 20px;
}

.doctor-image {
  width: 200rpx;
  height: 200rpx;
  margin-bottom: 10px;
  border: 4px solid white;

}

.doctor-name {
  font-size: 20px;
  font-weight: bold;
}

.doctor-specialty {
  font-size: 14px;
  color: gray;
}

.doctor-rating {
  display: flex;
  align-items: center;
  gap: 20rpx;
}

.live-badge {
  background-color: red;
  color: white;
  padding: 2px 5px;
  border-radius: 5px;
  font-size: 12px;
}

.rating {
  color: gold;
  font-size: 14px;
}

.form-group {
  margin-bottom: 20px;
}

.label {
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #333;
  display: block; /* Ensures label behaves as a block element */
}

.textarea {
  width: 100%;
  height: 60px;
  padding: 10px; /* Add padding inside the textarea */
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 14px;
  background-color: white;
  box-sizing: border-box; /* Ensure padding is included in the width/height calculation */
  resize: none; /* Prevent resizing if not needed */
}

.medical-record {
  display: flex;
  gap: 20px;
  margin-bottom: 20px;
}

.record-card,
.add-card {
  flex: 1;
  background-color: white;
  padding: 15px;
  border-radius: 10px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  align-items: flex-start;
  text-align: left;
}

.record-card {
  width: 60%;
}

.add-card {
  justify-content: center;
  align-items: center;
  text-align: center;
}

.heartcard {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}

.icon {
  width: 50px;
  height: 50px;
}

.record-label {
  font-size: 16px;
  font-weight: bold;
  color: black;
}

.record-value {
  font-size: 24px;
  font-weight: bold;
  margin-top: 10px;
  color: black;
}

.unit {
  font-size: 16px;
  color: gray;
}

.add-icon {
  width: 50px;
  height: 50px;
  margin-bottom: 10px;
}

.add-label {
  font-size: 16px;
  font-weight: bold;
  color: blue;
}

.select-date {
  margin-bottom: 20px;
}

.calendar {
  background-color: white;
  padding: 10px;
  border-radius: 10px;
  box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}


.select-time {
  margin-bottom: 20px;
}

.label {
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 10px;
  color: #333;
  display: block;
}

.time-slots {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.time-slot {
  flex: 1;
  text-align: center;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 30px; /* Increased border-radius for more rounded corners */
  cursor: pointer;
  transition: background-color 0.3s, color 0.3s;
  font-size: 14px;
}

.time-slot.selected {
  background-color: #0034EE; /* Blue background for selected state */
  color: white;
  border-color: #0034EE;
}
</style>