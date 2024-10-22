<script setup>
// Ontvang de berichten als props
const props = defineProps({
  messages: {
    type: Array,
    required: true,
  },
});
</script>

<template>
  <h2>Comments</h2>
  <ul>
    <li v-for="(message, index) in props.messages" :key="message._id">
      <strong>{{ message.user }}</strong>: {{ message.text }} <!-- Zorg ervoor dat deze properties correct zijn -->
    </li>
  </ul>
</template>

<style scoped>
/* Voeg hier je stijl toe als dat nodig is */
h2 {
  font-size: 24px;
}

ul {
  list-style-type: none; /* Verwijder de standaard opsommingstekens */
  padding: 0; /* Verwijder de standaard padding */
}

li {
  margin-bottom: 8px; /* Voeg wat ruimte toe tussen de berichten */
  border: 1px solid #ddd; /* Voeg een rand toe */
  padding: 10px; /* Voeg wat padding toe */
  border-radius: 4px; /* Maak de hoeken afgerond */
  background-color: #f9f9f9; /* Voeg een lichte achtergrondkleur toe */
}
</style>
