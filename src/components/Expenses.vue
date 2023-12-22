<template>
  <div class="bg-white flex justify-evenly mt-10 py-5">
    <div>
      <h1 class="uppercase">Income</h1>
      <p class="text-green-600">+${{ income }}</p>
    </div>
    <div class="border-l pl-12">
      <h1 class="uppercase">Expense</h1>
      <p class="text-red-600">${{ expenses }}</p>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
const props = defineProps({
  income: {
    type: Number,
    required: true
  },
  expenses: {
    type: Number,
    required: true
  }
});
</script>