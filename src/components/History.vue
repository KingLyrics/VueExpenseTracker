<template>
  <div class="mt-12 ">
    <h1 class="text-xl border-b border-b-gray-300 pb-2">History</h1>
    <div class="space-y-4">


      <!-- <div v-for="transaction in transactions" :key="transaction.id" class="bg-white flex justify-between mt-5 p-2" id="history-bar"
          :class="transaction.amount < 0 ? 'border-r-4 border-red-600' : 'border-r-4 border-green-600'">

          <p>{{ transaction.text }}</p>
          <p>${{ transaction.amount }}</p>
          <span class="delete-btn">X</span>

        </div> -->

      <div v-for="transaction in transactions" :key="transaction.id"
        class="bg-white flex justify-between mt-5 p-2 items-center" id="history-bar"
        :class="transaction.amount < 0 ? 'border-r-4 border-red-600' : 'border-r-4 border-green-600'">

        <p>{{ transaction.text }}</p>
        <p>${{ transaction.amount }}</p>
        <button @click="deleteTransaction(transaction.id)" class="delete-btn  group-hover:block">
          X
        </button>

      </div>


    </div>
  </div>
</template>

<script setup>

import { defineProps } from 'vue';
const props = defineProps({
  transactions: Array,
  required: true
});

const emit = defineEmits(['transactionDeleted'])

const deleteTransaction = (id) => {
  emit('transactionDeleted', id)
}


</script>

<style scoped>
.delete-btn {
  background-color: #e53e3e;
  color: #fff;
  padding: 5px 10px;
  cursor: pointer;
  border: none;
  outline: none;
  transition: background-color 0.3s ease;
}

.delete-btn:hover {
  background-color: #c53030;
}
</style>