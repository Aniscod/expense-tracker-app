<script setup>
import { computed } from 'vue';

// Define props
const props = defineProps({
  transactions: {
    type: Array,
    required: true
  }
});

// Computed properties for income and expenses
const income = computed(() => {
  return props.transactions
    .filter(transaction => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0);
});

const expenses = computed(() => {
  return props.transactions
    .filter(transaction => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0);
});
</script>

<template>
  <div class="inc-exp-container">
    <div>
      <h4>Income</h4>
      <p id="money-plus" class="money plus">{{ income }}$</p>
    </div>
    <div>
      <h4>Expenses</h4>
      <p id="money-minus" class="money minus">{{ expenses }}$</p>
    </div>
  </div>
</template>
