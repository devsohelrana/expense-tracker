<script setup>
import MainHeader from "@/components/MainHeader.vue";
import TotalBalance from "@/components/TotalBalance.vue";
import IncomeExpense from "@/components/IncomeExpense.vue";
import TransactionList from "@/components/TransactionList.vue";
import AddTransaction from "@/components/AddTransaction.vue";

import { ref, computed, onMounted } from 'vue'
import { toast } from "vue3-toastify";

const transactions = ref([]);

onMounted(() => {
  const saveTransactions = JSON.parse(localStorage.getItem('transactions'));
  if (saveTransactions) {
    transactions.value = saveTransactions;
  }
});

// Get total
const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount;
  }, 0);
});

// Get income
const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
});

// Get expenses
const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0).toFixed(2);
});


// Add transaction
const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionData.text,
    amount: transactionData.amount
  });

  saveTransactionsToLocalStorage();

  toast.success("Transaction added", {
    position: toast.POSITION.BOTTOM_RIGHT,
    autoClose: 5000,
  });

};

// auto id generate
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

// delete transaction
const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) =>
    transaction.id !== id);

  saveTransactionsToLocalStorage();

  toast.success("Transaction added", {
    position: toast.POSITION.BOTTOM_RIGHT,
    autoClose: 5000,
  });

};


// Save to localStorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem('transactions', JSON.stringify(transactions.value))
}

</script>

<template>
  <MainHeader />
  <div class="flex flex-col sm:flex-row justify-between gap-6">
    <div class="w-full sm:w-6/12">
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />

      <div class="w-full flex justify-center items-center">
        <img src="./assets/img/cash.svg" alt="" class="w-2/4">
      </div>
    </div>
    <div class="space-y-2 w-full sm:w-6/12">
      <TotalBalance :total="+total" />
      <IncomeExpense :income="+income" :expenses="+expenses" />
      <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
    </div>
  </div>
</template>

<style scoped></style>