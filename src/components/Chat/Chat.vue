<script setup>
import { ref, onMounted } from 'vue';
import ChatMessages from './ChatMessages.vue';
import ChatForm from './ChatForm.vue';

// Reactive array om berichten op te slaan
const messages = ref([]);

// Functie om een nieuw bericht toe te voegen aan de lijst
function addMessage(newMessage) {
  messages.value.push(newMessage);
}

// Haal de berichten op bij het laden van de component
onMounted(() => {
  fetch('https://build-challenge-3.onrender.com/api/v1/messages')
    .then(response => {
      if (!response.ok) {
        throw new Error('Failed to fetch messages');
      }
      return response.json();
    })
    .then(data => {
      console.log('Fetched messages:', data);
      // Voeg de berichten toe aan de reactive array
      messages.value = data.data.messages; // Zorg ervoor dat dit overeenkomt met je API-structuur
    })
    .catch(error => {
      console.error('Error fetching messages:', error);
    });
});
</script>

<template>
    <ChatMessages :messages="messages" />
    <ChatForm @message-sent="addMessage" />
</template>

<style scoped>
/* Voeg hier je stijl toe als dat nodig is */
</style>
