<template>
  <h1 class="text-3xl">Expense Tracker</h1>
  <div class="mt-10">
    <h1 class="text-gray-800 uppercase font-bold">Your Balance</h1>
    <p class="text-3xl font-light">${{ total }}</p>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
  total: {
    type: Number,
    required: true
  },

})

</script>