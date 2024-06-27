<template>
  <Header></Header>
  <div class="container">
    <Balance :total="total"></Balance>
    <IncomeExpense></IncomeExpense>
    <TransactionList :transactions="transactions"></TransactionList>
    <AddTransaction></AddTransaction>
  </div>
</template>

<script setup>
import Header from "./components/Header.vue";
import Balance from "./components/Balance.vue";
import IncomeExpense from "./components/IncomeExpense.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

import { ref, computed } from "vue";

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

// Pegar despesas
</script>
