<template>
  <div class="mt-10">
    <h1 class="text-xl border-b border-b-gray-300 pb-2">Add new transaction</h1>
    <form class="mt-4" @submit.prevent="onSubmit">
      <label class="block pb-2 ">Text</label>
      <input type="text" placeholder="Enter text..." class="w-full p-2" v-model.trim="text">
      <label class="block mt-4 pb-2 ">Amount <br>(negative-expense, positive-income)</label>
      <input type="text" placeholder="Enter amount..." class="w-full p-2" v-model.trim="amount">
      <button type="submit" class="w-full mt-3 py-2 text-white bg-purple-500">Add Transaction</button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';
const toast = useToast();


const text = ref('');
const amount = ref('');

const emit = defineEmits(['transactionSubmitted'])



const onSubmit = () => {

  if (!text.value || !amount.value) {
    toast.error('Both fields must be filled')
    return;
  }


  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value)
  }
  emit('transactionSubmitted', transactionData)


  text.value = '';
  amount.value = '';

};
</script>
