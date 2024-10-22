<script setup>
import { ref } from 'vue';

const user = ref('');  // Username input
const message = ref('');  // Message input

// Functie om het bericht te versturen naar de API
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
      // Hier kun je eventueel het bericht aan de lijst toevoegen als je wilt dat de lijst direct bijgewerkt wordt
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

</style>
