<template>
	<view class="content">
		<view class="confirmation-page">
		    <!-- Main Card -->
		    <view class="confirmation-card">
		      <!-- Success Icon -->
		      <view class="success-icon">
		        <image src="/static/success-icon.png" class="checkmark" />
		      </view>
		
		      <!-- Confirmation Text -->
		      <text class="confirmation-text">Your appointment has been made!</text>
		
		      <!-- Doctor Info -->
		      <view class="doctor-info">
		        <image src="/static/doctor2.png" class="doctor-image" />
		        <view class="doctor-details">
		          <text class="doctor-name">Dr. Richardson</text>
		          <text class="doctor-specialty">Immunologist</text>
		        </view>
		      </view>
		
		      <!-- Appointment Details -->
		      <view class="appointment-details">
		        <view class="detail">
		          <text class="label">Date</text>
		          <text class="value">7/12/2024</text>
		        </view>
		        <view class="detail">
		          <text class="label">Time</text>
		          <text class="value">08:00 am</text>
		        </view>
		      </view>
			  <button @click="redirectToPage">Confirm</button>
		    </view>
		  </view>
	</view>
</template>

<script setup>
import { ref } from "vue";

	
const redirectToPage = () => {
	console.log("Redirecting...");
	uni.reLaunch({
	  url: '/pages/telemedicine/index'
	});
};
</script>

<style>
	.confirmation-page {
	  display: flex;
	  justify-content: center;
	  align-items: center;
	  height: 100vh;
	  background: linear-gradient(180deg, #3A007B, #1E1B6C);
	  padding: 20px;
	}
	
	.confirmation-card {
	  background: #fff;
	  border-radius: 15px;
	  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.25);
	  width: 90%;
	  max-width: 400px;
	  text-align: center;
	  padding: 20px;
	}
	
	.success-icon {
	  margin-bottom: 20px;
	}
	
	.checkmark {
	  width: 50px;
	  height: 50px;
	}
	
	.confirmation-text {
	  font-size: 18px;
	  font-weight: bold;
	  color: #000;
	  margin-bottom: 20px;
	}
	
	.doctor-info {
	  display: flex;
	  align-items: center;
	  margin: 20px 0;
	  background: #f9f9f9;
	  border-radius: 10px;
	  padding: 10px;
	}
	
	.doctor-image {
	  width: 70px;
	  height: 70px;
	  margin-right: 20px;
	}
	
	.doctor-details {
	  display: flex;
	  flex-direction: column;
	  text-align: left;
	}
	
	.doctor-name {
	  font-size: 16px;
	  font-weight: bold;
	  color: #000;
	}
	
	.doctor-specialty {
	  font-size: 14px;
	  color: #666;
	}
	
	.appointment-details {
	  display: flex;
	  justify-content: space-around;
	  margin-top: 20px;
	}
	
	.detail {
	  display: flex;
	  flex-direction: column;
	  text-align: center;
	  margin-bottom: 30rpx;
	}
	
	.label {
	  font-size: 14px;
	  color: #666;
	}
	
	.value {
	  font-size: 16px;
	  font-weight: bold;
	  color: #000;
	}
</style>