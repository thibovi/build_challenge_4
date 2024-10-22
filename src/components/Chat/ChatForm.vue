<script setup>
import { ref } from 'vue'; // Vergeet niet om 'ref' te importeren

const emit = defineEmits(); // Geen import meer nodig voor defineEmits

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
      console.log('Message sent:', data);
      // Emit een event om het nieuwe bericht door te geven
      emit('message-sent', {
        _id: data.data.message._id, // Zorg ervoor dat je deze structuur gebruikt
        user: user.value,
        text: message.value,
      });
    })
    .catch(error => {
      console.error('Error sending message:', error);
    });

  // Wis de velden na het versturen van het bericht
  user.value = '';
  message.value = '';
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
/* Voeg hier je stijl toe als dat nodig is */
</style>
