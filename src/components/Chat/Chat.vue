<script setup>
import { ref, onMounted } from 'vue';
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';

// Reactive array to store messages
const messages = ref([]);

// Function to add a new message to the list
function addMessage(newMessage) {
  console.log('New message to be added:', newMessage); // Debug log
  messages.value.push(newMessage); // Add new message to the reactive array
}

// Fetch messages on component mount
onMounted(() => {
  fetch('https://build-challenge-3.onrender.com/api/v1/messages')
    .then(response => {
      if (!response.ok) {
        throw new Error('Failed to fetch messages');
      }
      return response.json();
    })
    .then(data => {
      console.log('Fetched messages:', data.data.messages); // Debug log
      messages.value = data.data.messages; // Assign messages from API to the reactive array
    })
    .catch(error => {
      console.error('Error fetching messages:', error);
    });
});
</script>

<template>
  <div>
    <ChatMessages :messages="messages" />
    <ChatForm @message-sent="addMessage" />
  </div>
</template>

<style scoped>
/* Add any styles needed */
</style>
