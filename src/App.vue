<template>
  <Header></Header>
  <div class="container">
    <Balance :total="+total"></Balance>
    <IncomeExpense :renda="+renda" :despesas="+despesas"></IncomeExpense>
    <TransactionList
      :transactions="transactions"
      @transactionDeleted="handleTrasactionDeleted"
    ></TransactionList>
    <AddTransaction
      @transactionSubmited="handleTransactionSubmited"
    ></AddTransaction>
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { useToast } from "vue-toastification";

import { ref, computed, onMounted } from "vue";

const toast = useToast();

const transactions = ref([]);

onMounted(() => {
  const savedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if (savedTransactions) {
    transactions.value = savedTransactions;
  }
});

// Pegar o total
const total = computed(() => {
  return transactions.value.reduce((acc, transactions) => {
    return acc + transactions.amount;
  }, 0);
});

// Pegar renda
const renda = computed(() => {
  return transactions.value
    .filter((transactions) => transactions.amount > 0)
    .reduce((acc, transactions) => {
      return acc + transactions.amount;
    }, 0)
    .toFixed(2);
});

// Pegar despesas
const despesas = computed(() => {
  return transactions.value
    .filter((transactions) => transactions.amount < 0)
    .reduce((acc, transactions) => {
      return acc + transactions.amount;
    }, 0)
    .toFixed(2);
});

// Adicionar transação
const handleTransactionSubmited = (transactionsData) => {
  transactions.value.push({
    id: generateUniqueId(),
    text: transactionsData.text,
    amount: transactionsData.amount,
  });

  saveTransactionsToLocalStorage();

  toast.success("Transição Adicionada");
};

// Gerar ID unico
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

// Deletar transacao
const handleTrasactionDeleted = (id) => {
  transactions.value = transactions.value.filter(
    (transactions) => transactions.id !== id
  );

  deleteTransactionsToLocalStorage(id);

  toast.success("Transação Deletada");
};

// Salvar no localstorage
const saveTransactionsToLocalStorage = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};

// Deletar transacao do localStorage
const deleteTransactionsToLocalStorage = (id) => {
  const transactions = JSON.parse(localStorage.getItem("transactions") ?? "[]");
  const indexOf = transactions.findIndex((item) => item.id === id);
  if (indexOf !== -1) {
    transactions.splice(indexOf, 1);
    localStorage.setItem("transactions", JSON.stringify(transactions));
  }
};
</script>
