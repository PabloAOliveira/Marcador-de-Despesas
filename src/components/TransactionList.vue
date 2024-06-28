<template>
  <h3>Histórico</h3>
  <ul id="list" class="list">
    <li
      v-for="transactions in transactions"
      :key="transactions.id"
      :class="transactions.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transactions.text }} <span>${{ transactions.amount }}</span
      ><button @click="deleteTransaction(transactions.id)" class="delete-btn">
        x
      </button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from "vue";

const emit = defineEmits(["transactionDeleted"]);

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const deleteTransaction = (id) => {
  emit("transactionDeleted", id);
};
</script>
