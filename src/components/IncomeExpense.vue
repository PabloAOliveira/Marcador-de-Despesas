<template>
  <div class="inc-exp-container">
    <div>
      <h4>Renda</h4>
      <p id="money-plus" class="money plus">+${{ renda }}</p>
    </div>
    <div>
      <h4>Despesa</h4>
      <p id="money-minus" class="money minus">-${{ despesas }}</p>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from "vue";

const props = defineProps({
  renda: {
    type: Number,
    required: true,
  },
  despesas: {
    type: Number,
    required: true,
  },
});
</script>
