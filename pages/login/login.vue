<template>
  <view class="container">
    <!-- Header Section -->
    <view class="header">
      <view class="logo-container">
        <image
          class="back-arrow"
          src="/static/arrow-left.png"
          @click="handleClickBack"
        />
        <image class="logo" src="/static/logo.png" />
      </view>
      <view class="text-container">
        <text class="title">{{ currentTitle }}</text>
        <text class="subtitle">{{ currentSubtitle }}</text>
      </view>
    </view>

    <!-- Dynamic Content Section -->
    <view class="content">
      <view v-if="step === 1">
        <!-- Step 1: Personalize Experience -->
        <view class="form">
          <input class="input" placeholder="Age" />
          <input class="input" placeholder="Gender" />
          <view class="dropdown">
            <text class="dropdown-placeholder">Fitness Goals</text>
            <image class="dropdown-icon" src="/static/home/arrow-down.png" />
          </view>
        </view>
      </view>

      <view v-else-if="step === 2">
        <!-- Step 2: Health Information -->
        <view class="form">
          <view class="row">
            <input class="input" placeholder="Height" />
            <input class="input" placeholder="Weight" />
          </view>
          <input class="input" placeholder="Medical Condition" />
          <input class="input" placeholder="Allergies" />
        </view>
      </view>

      <view v-else-if="step === 3">
        <!-- Step 3: Set Your Goals -->
        <view class="list">
         <view
           v-for="goal in goals"
           :key="goal.id"
           class="list-item"
           @click="selectGoal(goal.id)"
         >
           <view class="icon-container">
             <image :src="goal.icon" class="icon" />
           </view>
           <view class="info">
             <text class="goal-title">{{ goal.title }}</text>
             <text class="goal-description">{{ goal.description }}</text>
           </view>
           <image
             class="radio"
             :src="selectedGoal === goal.id ? '/static/checked.png' : '/static/checkbox.png'"
           />
         </view>
        </view>
      </view>
      
      <view v-else-if="step === 4">
        <!-- Step 4: Activity Level -->
        <view class="list">
          <view
            v-for="activity in activities"
            :key="activity.id"
            class="list-item"
            @click="selectActivity(activity.id)"
          >
            <view class="info">
              <text class="goal-title">{{ activity.title }}</text>
              <text class="goal-description">{{ activity.description }}</text>
            </view>
            <image
                    class="radio"
                    :src="selectedActivity === activity.id ? '/static/checked.png' : '/static/checkbox.png'"
                  />
          </view>
        </view>
      </view>
    </view>

    <!-- Footer Section -->
    <view class="footer">
      <button class="next-button" @click="handleNext">Next</button>
    </view>
  </view>
</template>

<script setup>

import { ref, computed } from 'vue';

const step = ref(1);
const selectedGoal = ref(null);
const selectedActivity = ref(null);

const stepsData = {
  1: {
    title: 'Personalize Experience',
    subtitle: 'Tell us about yourself to get personalized recommendations.',
  },
  2: {
    title: 'Health Information',
    subtitle: 'Help us understand your health better.',
  },
  3: {
    title: 'Set Your Goals',
    subtitle: 'What do you want to achieve?',
  },
  4: {
    title: 'Activity Level',
    subtitle: 'Typical daily physical exertion rate.',
  },
};

const currentTitle = computed(() => stepsData[step.value].title);
const currentSubtitle = computed(() => stepsData[step.value].subtitle);

const goals = [
  { id: 1, title: 'Lose Weight', description: 'Shed pounds with personalized plans.', icon: '/static/fire.png' },
  { id: 2, title: 'Build Muscle', description: 'Strengthen through targeted training.', icon: '/static/squat.png' },
  { id: 3, title: 'Improve Endurance', description: 'Boost stamina with cardio workouts.', icon: '/static/run.png' },
  { id: 4, title: 'Stay Healthy', description: 'Maintain wellness with balanced routines.', icon: '/static/broccili.png' },
  { id: 5, title: 'Get Fitter', description: 'Elevate heart health and fitness.', icon: '/static/cycle.png' },
];

const activities = [
  { id: 1, title: 'Sedentary', description: 'Minimal physical activity, mostly sitting.' },
  { id: 2, title: 'Lightly Active', description: 'Light exercise or daily walking.' },
  { id: 3, title: 'Moderately Active', description: 'Regular moderate exercise or sports.' },
  { id: 4, title: 'Very Active', description: 'Intense daily exercise or labor.' },
];

const handleNext = () => {
  if (step.value < 4) {
    step.value += 1;
  } else {
	uni.navigateTo({
		url: '/pages/login/logincompile'
	})
  }
};

const handleClickBack = () => {
  if (step.value === 1) {
    // Navigate to the login page if on step 1
    uni.navigateTo({
    	url: '/pages/login/login'
    })
  } else if (step.value > 1) {
    // Otherwise, go to the previous step
    step.value -= 1;
  }
};

const selectGoal = (id) => {
  selectedGoal.value = id;
};

const selectActivity = (id) => {
  selectedActivity.value = id;
};

</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  height: 100vh;
  background-color: #ffffff;
}
.logo-container {
  display: flex;
  align-items: center;
  width: 100%;
  margin-bottom: 10rpx; /* Space between logo-container and text-container */
}
.header {
  background-color: #2b1a88;
  padding: 20rpx;
  display: flex;
  flex-direction: column; /* Ensures stacked layout */
  align-items: center; /* Centers the logo */
  position: relative;
  height: 25%; /* Adjusted height for proportional spacing */
  justify-content: space-evenly;
}
.back-button {
  position: absolute;
  left: 20rpx;
  width: 40rpx;
  height: 40rpx;
  background-color: black;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  box-shadow: 0px 2rpx 4rpx rgba(0, 0, 0, 0.1);
}

.logo {
  width: 150rpx;
  height: 150rpx;
  margin-top: 20rpx; /* Adds spacing from the top */
  margin-bottom: 10rpx; /* Adds spacing between the logo and title */
  margin-left: 35%;
}

.content {
  flex: 1;
  padding: 40rpx;
}

.text-container {
  width: 100%;
  padding-left: 20rpx; /* Align text to the left */
  margin-top: 10rpx; /* Add space between the logo and text */
  display: flex;
  flex-direction: column; /* Stack the title and subtitle vertically */
  align-items: flex-start; /* Ensure both title and subtitle align to the left */
  margin-bottom: 20px;
}

.title {
  font-size: 36rpx;
  color: white;
  font-weight: bold;
  margin-bottom: 10rpx; /* Add spacing between title and subtitle */
}

.subtitle {
  font-size: 22rpx;
  color: #d0d0d0;
}
.form .input {
  width: 100%;
  height: 90rpx;
  margin-bottom: 20rpx;
  border: 1rpx solid #d8d8d8;
  border-radius: 50rpx;
  padding: 0 20rpx;
  font-size: 28rpx;
  box-sizing: border-box; /* Ensures padding is included within the width/height */
}

.dropdown {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 1rpx solid #d8d8d8;
  border-radius: 50rpx;
  height: 90rpx;
  padding: 0 20rpx;
}

.dropdown-placeholder {
  font-size: 28rpx;
  color: #8c8c8c;
}

.dropdown-icon {
  width: 20rpx; /* Adjust size of the icon */
  height: 20rpx; /* Keep the same as width for a square */
  margin-left: 10rpx; /* Optional: Add some spacing from the text */
}

.footer {
  padding: 20rpx;
  background-color: #ffffff;
  text-align: center;
}

.next-button {
  display: flex;
  width: 80%;
  height: 2.8125rem;
  background-color: #3724eb;
  color: #ffffff;
  font-size: 0.875rem;
  font-weight: bold;
  border-radius: 1.40625rem;
  justify-content: center;
  align-items: center;
}
.back-arrow{
	height: 20px;
	width: 20px;
}

.list-item {
  display: flex;
  align-items: center; /* Align items vertically */
  padding: 20rpx;
  border: 1rpx solid #d8d8d8;
  border-radius: 50rpx;
  margin-bottom: 20rpx;
  position: relative; /* Allows absolute positioning for the radio image */
}


.info {
  display: flex;
  flex-direction: column; /* Stack title and description */
  flex: 1; /* Allow the info section to take available space */
  margin-left: 5px;
}

.goal-title {
  font-size: 28rpx; /* Larger font for title */
  color: black;
  margin-bottom: 5rpx;
}

.goal-description {
  font-size: 12px; /* Smaller font for description */
  color: #818898;
  margin-top: 5rpx; /* Space between title and description */
}

.radio {
  width: 40rpx; /* Size of the radio button */
  height: 40rpx;
  position: absolute; /* Align it to the rightmost side */
  right: 20rpx; /* Position it with some spacing from the edge */
  top: 50%; /* Vertically center it */
  transform: translateY(-50%); /* Ensure proper vertical alignment */
}

.icon-container {
  display: flex;
  justify-content: center;
  align-items: center;
  background-color: #f2f3f5; /* Very light grey */
  width: 80rpx; /* Adjust the size to make it circular */
  height: 80rpx; /* Keep height equal to width for a perfect circle */
  border-radius: 50%; /* Makes it a circle */
}

.icon {
  width: 50rpx; /* Adjust the icon size */
  height: 50rpx;
}


</style>
