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
          <button class="finish-button" @click="routehome">Finish</button>
        </view>
      </view>

      <!-- Chat Section -->
      <view class="chat-section">
        <view
          v-for="(message, index) in chatMessages"
          :key="index"
          :class="[
            'chat-bubble',
            message.type === 'doctor' ? 'doctor-bubble' : 
            message.type === 'user' ? 'user-bubble' : 
            message.type === 'buttons' ? 'button-bubble' : 
            message.type === 'calendar' ? 'calendar-bubble' : '' 
          ]"
        >
          <!-- Render text messages -->
          <template v-if="message.type === 'doctor' || message.type === 'user'">
            {{ message.content }}
          </template>
        
          <!-- Render regular button messages -->
          <template v-if="message.type === 'buttons' && !message.isDateButtons">
            <view class="button-group">
              <button
                v-for="(button, i) in message.buttons"
                :key="i"
                class="reply-button"
                @click="handleReply(button)"
              >
                {{ button }}
              </button>
            </view>
          </template>

          <!-- Render date button messages -->
          <template v-if="message.isDateButtons & message.isReschedule">
            <view class="date-button-row" v-for="(pair, i) in chunkArray(message.buttons, 2)" :key="i">
              <button
                v-for="(button, j) in pair"
                :key="j"
                class="reply-button date-button"
                @click="handleReply(button)"
              >
                {{ button }}
              </button>
            </view>
          </template>
		  
		    <!-- Render calendar component -->
		    <template v-if="message.type === 'calendar'">
				<view class="calendar-bubble">
				  <customcal @update-date="handleCalendarDateSelection" />
				</view>
			  </template>
        </view>
      </view>

      <!-- Input Section -->
      <view class="input-section">
        <image src="/static/Appointment/Doc.png" class="home-icon" />
        <input type="text" placeholder="Type a message" class="chat-input" v-model="userInput" />
        <image src="/static/Appointment/sendbutton.png" class="send-icon" @click="sendMessage" />
      </view>
    </view>
  </view>
</template>
<script setup>
import { ref } from "vue";
import customcal from "@/components/customCalendar/index.vue"
const userInput = ref("");

// Helper function to split an array into chunks
const chunkArray = (array, chunkSize) => {
  const results = [];
  for (let i = 0; i < array.length; i += chunkSize) {
    results.push(array.slice(i, i + chunkSize));
  }
  return results;
};

// Reactive state for chat messages
const chatMessages = ref([
  { type: "doctor", content: "Good morning, I am Dr. Richardson's bot assistant." },
  { type: "doctor", content: "How can I help you today?" },
  {
    type: "buttons",
    buttons: ["Reschedule my appointment", "View doctor’s schedule"], // Regular buttons
  },
  { 
    type: "buttons", 
    buttons: ["07 December", "08 December", "10 December", "12 December"], 
    isDateButtons: true, // Identify as date buttons
	isReschedule: false,
  },
]);

// Handle button reply
const handleReply = (reply) => {
  chatMessages.value.push({ type: "user", content: reply });

  if (reply === "Reschedule my appointment") {
    chatMessages.value.push({ type: "doctor", content: "When is your new appointment date?" });
    chatMessages.value.push({ type: "doctor", content: "Here are the recommendations for you:" });
    chatMessages.value.push({
      type: "buttons",
      buttons: ["07 December", "08 December", "10 December", "12 December"],
      isDateButtons: true,
      isReschedule: true,
    });
    chatMessages.value.push({ type: "doctor", content: "Not suitable for you?" });
    chatMessages.value.push({
      type: "buttons",
      buttons: ["Select another Date"],
    });
  } else if (reply === "View doctor’s schedule") {
    chatMessages.value.push({ type: "doctor", content: "Here is the doctor's schedule for the week." });
  } else if (reply === "Select another Date") {
    chatMessages.value.push({ type: "calendar" }); // Add a calendar message
  } else if (["07 December", "08 December", "10 December", "12 December"].includes(reply)) {
    // Handle date button selection
    chatMessages.value.push({ type: "doctor", content: "Thank you, your new appointment date has been created." });
    chatMessages.value.push({ type: "doctor", content: "And has been forwarded to the doctor." });
    chatMessages.value.push({ type: "doctor", content: "Have a nice day." });
  }
};

const handleCalendarDateSelection = (date) => {
  // Add the selected date to the chat messages
  chatMessages.value.push({ type: "user", content: date });

  // Add a confirmation message from the doctor
  chatMessages.value.push({ type: "doctor", content: "Thank you, your new appointment date has been created." });
  chatMessages.value.push({ type: "doctor", content: "And has been forwarded to the doctor." });
  chatMessages.value.push({ type: "doctor", content: "Have a nice day." });
};

// Handle user input
const sendMessage = () => {
  if (userInput.value.trim()) {
    chatMessages.value.push({ type: "user", content: userInput.value });
    userInput.value = ""; // Clear input field
  }
};

const routehome = () => {
	uni.reLaunch({
	  url: '/pages/telemedicine/index'
	});
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
  width: 100%; /* Ensure the chat section spans the full width */
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
  background-color: #605EF0;
  color: white;
  align-self: flex-end;
}

.reply-button {	
  align-self: flex-start;
  width: auto; /* Auto width for dynamic sizing */
  background-color: #0034EE;
  color: white;
  border: none;
  border-radius: 20px;
  font-size: 14px;
  font-weight: bold;
  text-align: center;
  cursor: pointer;
  margin: 0;
}


.button-group {
  display: flex;
  flex-direction: column;
  gap: 10px;
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

.button-bubble {
  width: 100%; /* Full width */
  padding: 10px 0; /* Remove left and right padding */
  border-radius: 0; /* Remove border radius if needed */
  align-self: stretch; /* Ensure the bubble spans the full width */
}

.date-button-row {
  display: flex;
  justify-content: space-between; /* Space buttons evenly */
  gap: 10px; /* Add space between buttons */
  margin-bottom: 10px; /* Add spacing between rows */
}

.date-button {
  flex: 1; /* Equal size for each button */
  background-color: #0034EE;
  color: white;
  border: none;
  border-radius: 20px;
  font-size: 14px;
  font-weight: bold;
  text-align: center;
  cursor: pointer;
  transition: background-color 0.3s;
}
.calendar-bubble {
  width: 100%; /* Ensure it takes up the full width of the chat section */
  max-width: none; /* Remove any max-width restriction */
  border-radius: 0; /* Remove border radius */
  padding: 0; /* Remove padding for proper alignment */
  background-color: transparent; /* Keep background transparent to match container */
  align-self: stretch; /* Ensure it spans across the full width */
  background: white;
  border-radius: 25px;
}

</style>