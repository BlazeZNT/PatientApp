<template>
	<view class="content">
		<view class="header">
		  <view class="header-left">
			<image src="/static/arrow-left.png" class="back-arrow" @click="goBack"/>
		  </view>
		  <text class="title">Appointment</text>
		  <view class="header-right">
			<image src="/static/bell.png" class="bell-icon" />
		  </view>
		</view>
	  <view class="form-page">
		<!-- Name -->
		<view class="form-group">
		  <text class="label">Name</text>
		  <input type="text" class="input" placeholder="Enter your name" v-model="formData.name" />
		</view>

		<!-- Birth Date / Age -->
		<view class="form-group">
		  <text class="label">Birth Date / Age</text>
		  <input type="text" class="input" placeholder="Enter your birth date and age" v-model="formData.birthDateAge" />
		</view>

		<!-- Email -->
		<view class="form-group">
		  <text class="label">Email</text>
		  <input type="email" class="input" placeholder="Enter your email" v-model="formData.email" />
		</view>

		<!-- Phone Number -->
		<view class="form-group">
		  <text class="label">Phone Number</text>
		  <input type="text" class="input" placeholder="Enter your phone number" v-model="formData.phoneNumber" />
		</view>

		<!-- Address -->
		<view class="form-group">
		  <text class="label">Address</text>
		  <input type="text" class="input" placeholder="Enter your address" v-model="formData.address" />
		</view>
		<h2>Patient Info</h2>
		<!-- Patient Info -->
		<view class="patient-info">
		      <!-- Weight Card -->
		      <view class="info-card">
		        <text class="info-label">Weight</text>
		        <view class="info-value">
		          <text class="value">{{ formData.weight }}</text>
		          <text class="unit">kg</text>
		        </view>
		      </view>
		      <!-- Height Card -->
		      <view class="info-card">
		        <text class="info-label">Height</text>
		        <view class="info-value">
		          <text class="value">{{ formData.height }}</text>
		          <text class="unit">cm</text>
		        </view>
		      </view>
		    </view>
		<view class="footer">
			<mybutton text="Book An Appointment" class="appointment-button" @click="handleNextClick" />
		  </view>
	  </view>
  </view>
</template>

<script setup>
import { reactive } from "vue";
import mybutton from "@/components/button/index.vue"

const formData = reactive({
  name: "",
  birthDateAge: "",
  email: "",
  phoneNumber: "",
  address: "",
  weight: 65,
  height: 175,
});

const goBack = () => {
	uni.redirectTo({
	  url: '/pages/telemedicine/index'
	});
};

const handleNextClick = () => {
	uni.navigateTo({
	  url: '/pages/telemedicine/doctordetails'
	});
};
</script>

<style scoped>
.content {
  min-height: 100vh; /* Ensures content takes the full viewport height */
  display: flex; /* Use Flexbox for layout */
  flex-direction: column; /* Arrange children in a column */
  background-color: #f5f5f5;
}

.form-page {
  flex: 1; /* Allow this section to take up remaining space */
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 15px;
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

.form-group {
  margin-bottom: 20px;
}

.label {
  font-size: 16px;
  font-weight: bold;
  margin-bottom: 5px;
  color: #333;
  display: block;
}

.input {
  width: 100 vw;
  padding: 10px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #fff;
}

.patient-info {
  display: flex;
  justify-content: space-between;
  gap: 20px;
}

.info-group {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.info-input {
  display: flex;
  align-items: center;
  margin-top: 10px;
}

.input-small {
  width: 60px;
  padding: 5px;
  font-size: 14px;
  text-align: center;
  border: 1px solid #ccc;
  border-radius: 5px;
  background-color: #fff;
}

.unit {
  font-size: 18px;
  color: #888888;
  margin-left: 5px;
}

.info-card {
  flex: 1;
  background-color: #fff;
  border-radius: 15px;
  box-shadow: 0px 4px 8px rgba(0, 0, 0, 0.1);
  padding: 20px;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.info-label {
  font-size: 16px;
  font-weight: bold;
  color: #000;
  margin-bottom: 10px;
}

.info-value {
  display: flex;
  align-items: baseline;
}

.value {
  font-size: 28px;
  font-weight: bold;
  color: #000;
}
</style>