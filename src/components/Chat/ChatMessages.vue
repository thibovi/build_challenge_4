<script setup>
import { onMounted, reactive } from 'vue';

const messages = reactive([]);

// Haal de berichten op zodra de component geladen wordt
onMounted(() => {
  fetch('https://build-challenge-3.onrender.com/api/v1/messages')
    .then(response => {
      if (!response.ok) {
        throw new Error('Failed to fetch messages');
      }
      return response.json();
    })
    .then(data => {
      // Voeg de berichten toe aan de reactive array
      messages.push(...data.data.messages);
    })
    .catch(error => {
      console.error('Error fetching messages:', error);
    });
});
</script>

<template>
  <h2>Comments</h2>
  <ul>
    <li v-for="message in messages" :key="message._id">
      <strong>{{ message.user }}</strong>: {{ message.text }}
    </li>
  </ul>
</template>

<style scoped>

</style>
