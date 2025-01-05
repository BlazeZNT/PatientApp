<template>
	<view class="content">
	  <view class="consultation-page">
		<!-- Header -->
		<view class="header">
		  <view class="doctor-info">
		    <view class="doctor-image-container">
		      <image src="/static/doctor2.png" class="doctor-image" />
		      <view class="green-dot"></view>
		    </view>
		    <view class="docstuff">
		      <text class="doctor-name">Dr. Richardson</text>
		      <text class="doctor-specialty">Immunologist</text>
		    </view>
		  </view>
		  <view class="header-button">
			  <button class="video" @click="handleNextClick">
			    <image src="/static/video.png" alt="Video Icon" class="button-icon" />
			  </button>
			  <button class="finish-button">Finish</button>
		  </view>
		</view>

		<!-- Chat Section -->
		<view class="chat-section">
		  <view class="chat-bubble doctor-bubble">Good morning, I am Dr. Richardson</view>
		  <view class="chat-bubble doctor-bubble">Can I help you?</view>
		  <view class="chat-bubble user-bubble">Hi doctor</view>
		  <view class="chat-bubble user-bubble">My chest feels very hurt</view>
		  
		  <view class="chat-bubble doctor-bubble">Oh got it. </view>
		  <view class="chat-bubble doctor-bubble">Can you share your heart rate?</view>

		  <!-- Heart Rate Card -->
		  <view class="record-card user-bubble">
		    <view class="heartcard">
		      <text class="record-label">Heart Rate</text>
		      <image src="/static/appointment/heartbeat.png" alt="heart" class="icon" />
		    </view>
		    <text class="record-value">120 <text class="unit">bpm</text></text>
		  </view>

		  <view class="chat-bubble doctor-bubble">It looks great, seems like you just feel tired.</view>
		  <view class="chat-bubble doctor-bubble">I will create some prescription for you.</view>

		  <!-- Prescription Card -->
		  <view class="prescription-card">
			<text class="card-title">Mr. Brian’s Prescription</text>
			<view class="medicine-box">
				<image src="/static/appointment/medicine2.png" alt="heart" class="icon" />
				<view class="prescription-item">Antacids</view>
			</view>
			<view class="medicine-box">
				<image src="/static/appointment/medicine1.png" alt="heart" class="icon" />
				<view class="prescription-item">Simethicone</view>
			</view>
			<button class="get-medicine-button">Get Medicine</button>
		  </view>
		</view>

		<!-- Input Section -->
		<view class="input-section">
		  <image src="/static/Appointment/Doc.png" class="home-icon" />
		  <input type="text" placeholder="Type a message" class="chat-input" />
		  <image src="/static/Appointment/sendbutton.png" class="send-icon" />
		</view>
	  </view>
	</view>
</template>

<script setup>
	const handleNextClick = () => {
		uni.redirectTo({
			url: '/pages/telemedicine/video'
		})
	}
</script>

<style scoped>
.consultation-page {
  display: flex;
  flex-direction: column;
  height: 100vh;
  background-color: #f5f5f5;
}

.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 20px;
  background-color: white;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  padding-top: 40px;
}

.docstuff{
	display: flex;
	flex-direction: column;
}

.header-button{
	display: flex;
	flex-direction: row;
	gap: 2px;
	align-items: center;
}

.finish-button {
  display: flex;
  background-color: red;
  border-radius: 15px; /* Slightly less rounded for slimmer appearance */
  font-weight: bold;
  font-size: 12px; /* Reduced font size */
  padding: 5px 10px; /* Reduced padding for slimmer button */
  min-width: 60px; /* Optional: Define a minimum width */
  max-height: 30px;
  text-align: center;
  justify-content: center;
  align-items: center;
  color: white;
}

.video{
  display: flex;
  background-color: #DBEDFF;
  border-radius: 15px; /* Slightly less rounded for slimmer appearance */
  font-weight: bold;
  font-size: 12px; /* Reduced font size */
  padding: 5px 10px; /* Reduced padding for slimmer button */
  width: auto;
  max-height: 30px;
  text-align: center;
  justify-content: center;
  color: white;
}

.button-icon {
  width: 20px;
  height: 20px;
}

.doctor-info {
  display: flex;
  align-items: center;
  gap: 10px;
}

.doctor-image-container {
  position: relative; /* Parent container for the green dot */
  width: 50px;
  height: 50px;
}

.doctor-image {
  width: 100%;
  height: 100%;
}

.green-dot {
  position: absolute;
  width: 10px;
  height: 10px;
  background-color: #00ff00; /* Green color */
  border-radius: 50%;
  bottom: -3px; /* Adjust positioning */
  right: -3px; /* Adjust positioning */
  border: 2px solid white; /* Optional border for better contrast */
}

.doctor-name {
  font-size: 16px;
  font-weight: bold;
}

.doctor-specialty {
  font-size: 14px;
  color: gray;
}



.chat-section {
  flex: 1;
  padding: 20px;
  display: flex;
  flex-direction: column;
  gap: 10px;
  overflow-y: auto;
}

.chat-bubble {
  max-width: 70%;
  padding: 10px 15px;
  border-radius: 20px;
  font-size: 14px;
  line-height: 20px;
}

.doctor-bubble {
  background-color: #f0f0f0;
  align-self: flex-start;
}

.user-bubble {
  background-color: blue;
  color: white;
  align-self: flex-end;
}


.card-content {
  display: flex;
  align-items: center;
  gap: 10px;
}

.card-title {
  font-size: 16px;
  font-weight: bold;
}


.card-value {
  font-size: 24px;
  font-weight: bold;
}

.unit {
  font-size: 16px;
  color: gray;
}

.prescription-card {
  background-color: white;
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin: 10px auto;
  width: 100%;
}

.prescription-item {
  margin-left: 10px;
  font-size: 14px;
  color: black;
}

.get-medicine-button {
  background-color: blue;
  color: white;
  border-radius: 20px;
  font-size: 14px;
  text-align: center;
  font-weight: bold;
}

.medicine-box{
	display: flex;
	flex-direction: row;
	align-items: center;
}
.medicine-box:first-of-type {
  padding-bottom: 10px;
  border-bottom: 1px dotted #ccc;
}

.input-section {
  display: flex;
  align-items: center;
  padding: 10px 20px;
  background-color: white;
  box-shadow: 0 -2px 5px rgba(0, 0, 0, 0.1);
  gap: 10px;
}

.home-icon {
  width: 40px;
  height: 40px;
}

.chat-input {
  flex: 1;
  padding: 10px;
  border: 1px solid #ccc;
  border-radius: 20px;
}

.send-icon {
  width: 24px;
  height: 24px;
}

.record-card{
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
  width: 45%;
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

uni-button:after {
    content: none !important;
}

</style>