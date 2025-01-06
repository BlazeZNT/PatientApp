<template>
	<view class="content">
		<view class="header">
		  <view class="header-left">
			<image src="/static/arrow-left.png" class="back-arrow" @click="goBack"/>
		  </view>
		  <text class="title">Reschedule</text>
		  <view class="header-right">
			<image src="/static/bell.png" class="bell-icon" />
		  </view>
		</view>
		<view class="containerbox">
			<!-- Doctor Info Section -->
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
			<mybutton text="Submit" class="appointment-button" @click="handleNextClick" />
			<mybutton text="Chat to doctor's assistant" class="assistant-button" @click="goaichat" />
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
const timeSlots = ["08:00", "10:00", "14:00", "16:00","18:00", "20:00", "22:00", "24:00"];
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

const goaichat = () => {
	uni.navigateTo({
		url: '/pages/telemedicine/reschedule/aichat'
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
  flex-wrap: wrap; /* Allows wrapping to the next line */
  gap: 10px; /* Spacing between buttons */
  justify-content: space-between; /* Adjust spacing between items */
}

.time-slot {
  width: calc(25% - 10px); /* Ensure 4 buttons fit per row with gap adjustment */
  text-align: center;
  background-color: #f5f5f5;
  border: 1px solid #ccc;
  border-radius: 30px;
  cursor: pointer;
  transition: background-color 0.3s, color 0.3s;
  font-size: 14px;
  padding: 0; /* Adjust for better button height */
  box-sizing: border-box; /* Ensure padding is included in the button width */
  color: black;
}

.time-slot.selected {
  background-color: #0034EE;
  color: white;
  border-color: #0034EE;
}

.appointment-button{
	margin-bottom: 10px;
}

.assistant-button{
	color: #0034EE;
	background-color: white;
}
</style>