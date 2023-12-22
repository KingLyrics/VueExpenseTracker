<template>
  <div class="bg-gray-100 min-h-screen">
    <div class="max-w-md mx-auto p-9 lg:pt-11">

      <!-- Balance and title -->
      <Header :total="+total" />
      <!-- Balance and title end -->


      <!-- Income/Expense -->
      <Expenses :income="+income" :expenses="+expenses" />
      <!-- Income/Expense end -->

      <!-- History Section  -->

      <History :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
      <!-- History Section end -->


      <!-- Transaction section -->
      <Transaction @transactionSubmitted="handleTransactionSubmitted" />
      <!-- Transaction section end-->

    </div>


  </div>
</template>

<script setup>
import Header from './components/Header.vue'
import Expenses from './components/Expenses.vue'
import History from './components/History.vue'
import Transaction from './components/Transaction.vue'

import { ref, computed, onMounted } from 'vue'
import { useToast } from 'vue-toastification';

const toast = useToast()

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem('transactions'))

  if (savedTransactions) {
    transactions.value = savedTransactions
  }
})


const total = computed(() => {
  const rawTotal = transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);

  return parseFloat(rawTotal.toFixed(2));
});

const income = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return transaction.amount > 0 ? acc + transaction.amount : acc;
  }, 0);

})

const expenses = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return transaction.amount < 0 ? acc + transaction.amount : acc;
  }, 0);
});

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  })
  saveToLocalStorage();
  toast.success('Transaction Added!')
}

const generateUniqueId = () => {
  return Math.floor(Math.random() * 100)
}

const handleTransactionDeleted = (transactionId) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== transactionId)
  toast.success('Transaction Deleted')
};

const saveToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}


</script>