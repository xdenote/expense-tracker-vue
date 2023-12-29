<script setup>
import Header from "@/components/Header.vue";
import Balance from "@/components/Balance.vue";
import IncomeExpenses from "@/components/IncomeExpenses.vue";
import TransactionList from "@/components/TransactionList.vue";
import AddTransactions from "@/components/AddTransactions.vue";
import {ref, computed, onMounted} from "vue";
import {useToast} from "vue-toastification";

const toast = useToast();

const transactions = ref([]);

onMounted(async () => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));
  if(savedTransactions) {
    transactions.value = savedTransactions;
  }
});

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => (acc += transaction.amount), 0).toFixed(2);
});

const income = computed(() => {
  return transactions.value.filter((transaction) => transaction.amount > 0).reduce((acc, transaction) => (acc += transaction.amount), 0).toFixed(2);
});

const expense = computed(() => {
  return transactions.value.filter((transaction) => transaction.amount < 0).reduce((acc, transaction) => (acc += transaction.amount), 0).toFixed(2);
});

const handleTransaction = (transaction) => {
  transactions.value.push(transaction);
  toast.success("Transaction added successfully");
  saveTransactions();
  console.log(transactions.value);
};

const deletedTransaction = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id);
  toast.success("Transaction deleted successfully");
  saveTransactions();
  console.log(transactions.value);
};

//save to local storage
const saveTransactions = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};

</script>

<template>
  <Header/>
  <div class="container">
    <Balance :total="+total"/>
    <IncomeExpenses :income="+income" :expense="+expense"/>
    <TransactionList :transactions="transactions" @transactionDeleted="deletedTransaction"/>
    <AddTransactions @addTransaction="handleTransaction"/>
  </div>
</template>