<template>
  <h3>Adicionar Nova Transação</h3>
  <form id="form" @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Descrição</label>
      <input
        type="text"
        id="text"
        v-model="text"
        placeholder="Digite a descrição..."
      />
    </div>
    <div class="form-control">
      <label for="amount"
        >Quantia <br />
        (Negativo - despesa, Positivo - renda)</label
      >
      <input
        type="text"
        id="amount"
        v-model="amount"
        placeholder="Insira o valor..."
      />
    </div>
    <button class="btn">Adicionar Transação</button>
  </form>
</template>

<script setup>
import { ref } from "vue";
import { useToast } from "vue-toastification";

const emit = defineEmits(["transactionSubmited"]);

const toast = useToast();

const text = ref("");
const amount = ref("");
// valida para todos os campos estarem preenchidos ao enviar o form
const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error("Ambos os campos devem ser preenchidos");
    return;
  }

  const transactionsData = {
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("transactionSubmited", transactionsData);

  text.value = "";
  amount.value = "";
};
</script>
