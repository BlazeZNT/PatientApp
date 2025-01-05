<template>
  <button class="next-button" @click="handleClick">
    {{ text }}
  </button>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue';

// Define props
defineProps({
  text: {
    type: String,
    required: true, // Make it mandatory to provide the button text
  },
});

// Define emits
const emit = defineEmits(['click']);

// Emit the click event when the button is clicked
const handleClick = () => {
  emit('click');
};
</script>

<style scoped>
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
  cursor: pointer; /* Add pointer cursor for better UX */
}
</style>