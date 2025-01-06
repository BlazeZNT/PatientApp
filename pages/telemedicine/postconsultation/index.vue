<template>
	<view class="content">
		<view class="header">
			<view class="header-left">
				<image src="/static/arrow-left.png" class="back-arrow" @click="goBack" />
			</view>
			<text class="title">Post Consultation</text>
			<view class="header-right">
				<image src="/static/Appointment/share.png" class="bell-icon" />
			</view>
		</view>
		<view class="form-page">
			<!-- Doctor Information -->
			<view class="doctor-info">
				<image src="/static/doctor2.png" class="doctor-image" />
				<view class="doctor-details">
					<text class="doctor-name">Dr. Richardson</text>
					<text class="doctor-specialty">Immunologist</text>
				</view>
			</view>

			<!-- Date & Time Consultation -->
			<view class="form-group">
				<text class="label">Date & Time Consultation</text>
				<view class="data-box">07 December, 2024 ・10:00 am</view>
			</view>

			<!-- Complaints -->
			<view class="form-group">
				<text class="label">Complaints</text>
				<view class="data-box">
					• Fever with Chills 4 days<br />
					• Headache 2 days
				</view>
			</view>

			<!-- Diagnosis -->
			<view class="form-group">
				<text class="label">Diagnosis</text>
				<view class="data-box">
					The viruses that cause flu spread at high levels during certain times of the year in the Northern
					and Southern hemispheres. These are called flu seasons. During times when flu is widespread, you
					may not need a flu test.
				</view>
			</view>

			<!-- Advice -->
			<view class="form-group">
				<text class="label">Advice</text>
				<view class="data-box">
					• Take a rest<br />
					• Get disciplined with taking medicine on prescription
				</view>
			</view>
			<view class="form-group">
				<text class="label">Prescription</text>
				<view class="medicine-group">
					<view class="medicine-box">
						<image src="/static/appointment/medicine2.png" alt="heart" class="icon" />
						<view class="medicine-text">
							<view class="prescription-item title2">Antacids</view>
							<view class="prescription-item ">1 morning, 1 night (before food)</view>
							<view class="prescription-item ">Duration: 30 days</view>
						</view>
					</view>
					<view class="medicine-box">
						<image src="/static/appointment/medicine1.png" alt="heart" class="icon" />
						<view class="medicine-text">
							<view class="prescription-item title2">Simethicone</view>
							<view class="prescription-item ">1 morning, 1 night (before food)</view>
						</view>
					</view>
				</view>
			</view>
			
			<!-- Follow Up Date -->
			<view class="form-group">
				<text class="label">Follow up date</text>
				<view class="data-box">12-12-2024</view>
			</view>
			
			<view class="form-group">
				<text class="label">Signature</text>
				<view class="data-box signature-box">
					<image src="/static/appointment/robertson.png" class="signature-image" />
				</view>
			</view>
			<view class="footer">
			    <!-- Primary Button -->
			    <view class="appointment-button" @click="handleNextClick">
			        <text>Consult Again</text>
			    </view>
			
			    <!-- Secondary Buttons -->
			    <view class="buttonpack">
			        <view class="recordbtn">
			            <image src="/static/appointment/rewind.png" class="button-icon" />
			            <text>Consult Again</text>
			        </view>
			        <view class="recordbtn">
			            <image src="/static/appointment/cloud.png" class="button-icon" />
			            <text>Export to pdf</text>
			        </view>
			    </view>
			</view>
		</view>
	</view>
</template>

<script setup>
import mybutton from "@/components/button/index.vue"
const goBack = () => {
	uni.redirectTo({
		url: '/pages/telemedicine/index',
	});
};
</script>

<style scoped>
.content {
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    background-color: #f6f7f8;
}

.form-page {
    flex: 1;
    padding: 20px;
    display: flex;
    flex-direction: column;
    background-color: white;
    gap: 5px;
}

.header {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 20rpx;
    padding-top: 30px;
    background-color: white;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

.header-left,
.header-right {
    display: flex;
    align-items: center;
}

.title {
    flex: 1;
    text-align: center;
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
    margin-bottom: 10px;
    color: #333;
    display: block;
}

.data-box,
.doctor-info,
.medicine-box {
    background-color: #F9FBFD;
    border-radius: 10px;
    padding: 10px;
}

.data-box {
    padding: 10px 15px;
    font-size: 14px;
    color: #333;
    line-height: 1.6;
    border: 1px solid #e0e0e0;
}

.doctor-info {
    display: flex;
    align-items: center;
    margin: 20px 0;
}

.doctor-image {
    width: 80px;
    height: 80px;
    border: 5px solid white;
    border-radius: 20px;
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

.icon {
    width: 60px;
    height: 60px;
}

.medicine-box {
    display: flex;
    flex-direction: row;
    align-items: center;
    box-shadow: 0px 2px 5px rgba(0, 0, 0, 0.1);
}

.prescription-item {
    margin-left: 20px;
    font-size: 14px;
}

.medicine-group {
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.medicine-text {
    display: flex;
    flex-direction: column;
}

.title2 {
    margin-bottom: 5px;
}

.signature-image {
    width: 110px;
    height: 37px;
}

.footer {
    width: 100%;
    margin-top: auto;
    padding: 10px;
    display: flex;
    flex-direction: column;
    gap: 10px;
}

.appointment-button,
.recordbtn {
    display: flex;
    align-items: center;
    justify-content: center;
    border: none;
    border-radius: 10px;
}

.appointment-button {
    width: 100%;
    background-color: #0034ee;
    color: white;
    padding: 15px;
    font-size: 16px;
    font-weight: bold;
    cursor: pointer;
}

.recordbtn {
    width: 48%;
    background-color: whitesmoke;
    color: #0034ee;
    padding: 10px;
    font-size: 14px;
    font-weight: bold;
    gap: 10px;
    cursor: pointer;
}

.buttonpack {
    width: 100%;
    margin-top: 10px;
    display: flex;
    gap: 10px;
    justify-content: space-between;
}

.button-icon {
    width: 20px;
    height: 20px;
}
</style>