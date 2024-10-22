<script setup>
import { defineProps } from 'vue';

// Receive messages as props
const props = defineProps({
  messages: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <h2>Messages</h2>
  <ul>
    <li v-for="(message, index) in props.messages" :key="message._id">
      <strong>{{ message.user }}</strong>: {{ message.text }}
    </li>
  </ul>
</template>

<style scoped>
/* Add styles if needed */
</style>
