<template>
  <Header></Header>
  <div class="container">
    <Balance :total="+total"></Balance>
    <IncomeExpense :renda="+renda" :despesas="+despesas"></IncomeExpense>
    <TransactionList :transactions="transactions"></TransactionList>
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

import { ref, computed } from "vue";

const toast = useToast();

const transactions = ref([
  { id: 1, text: "Flower", amount: -19.99 },
  { id: 2, text: "Salario", amount: 200.99 },
  { id: 3, text: "Livros", amount: -10.99 },
  { id: 4, text: "FreeLance", amount: 150 },
]);

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

  toast.succes("Transição Adicionada");
};

// Gerar ID unico
const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};
</script>
