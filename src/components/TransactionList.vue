<template>
  <h3>Histórico</h3>
  <ul id="list" class="list">
    <li
      v-for="transactions in transactions"
      :key="transactions.id"
      :class="transactions.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transactions.text }} <span>${{ transactions.amount }}</span
      ><button class="delete-btn">x</button>
    </li>
  </ul>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});
</script>
