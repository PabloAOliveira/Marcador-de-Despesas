<template>
  <h3>Adicionar Nova Transação</h3>
  <form id="form">
    <div class="form-control">
      <label for="text">Descrição</label>
      <input type="text" id="text" placeholder="Digite a descrição..." />
    </div>
    <div class="form-control">
      <label for="amount"
        >Quantia <br />
        (Negativo - despesa, Positivo - renda)</label
      >
      <input type="number" id="amount" placeholder="Insira o valor..." />
    </div>
    <button class="btn">Adicionar Transação</button>
  </form>
</template>
