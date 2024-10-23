<script setup>
import { ref } from 'vue';

const emit = defineEmits();

const user = ref('');  // Username input
const message = ref('');  // Message input

function sendMessage() {
  if (!user.value || !message.value) {
    alert('Both username and message are required');
    return;
  }

  fetch('https://build-challenge-3.onrender.com/api/v1/messages', {
    method: 'POST',
    headers: {
      'Content-Type': 'application/json',
    },
    body: JSON.stringify({
      message: {
        user: user.value,
        text: message.value,
      },
    }),
  })
    .then(response => {
      if (!response.ok) {
        throw new Error('Failed to send message');
      }
      return response.json();
    })
    .then(data => {
      console.log('Message sent:', data); // Debug log

      // Emit an event to pass the new message to the parent
      emit('message-sent', {
        _id: data.data.message._id, // Use the correct ID from the API
        user: user.value,
        text: message.value,
      });

      // Clear input fields after sending the message
      user.value = '';
      message.value = '';
    })
    .catch(error => {
      console.error('Error sending message:', error);
    });
}
</script>

<template>
  <div class="form">
    <input v-model="user" type="text" placeholder="Your name" />
    <input v-model="message" type="text" placeholder="Type your message here" />
    <button @click="sendMessage">Send</button>
  </div>
</template>

<style scoped>
/* Add styles if needed */
</style>
