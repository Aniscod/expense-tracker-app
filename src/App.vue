<script setup>
import Header from './components/Header.vue';
import Balance from './components/Balance.vue';
import IncomeExpensis from './components/IncomeExpensis.vue';
import TransactionList from './components/TransactionList.vue';
import AddTransaction from './components/AddTransaction.vue';

import { ref,computed,watch  } from 'vue';

import { useToast } from 'vue-toastification';

const toast = useToast()

// Function to load transactions from local storage
const loadTransactions = () => {
    const savedTransactions = localStorage.getItem('transactions');
    return savedTransactions ? JSON.parse(savedTransactions) : [];
};

// Create a reactive transactions ref
const transactions = ref(loadTransactions());

// Watch for changes and save to local storage
watch(transactions, (newTransactions) => {
    localStorage.setItem('transactions', JSON.stringify(newTransactions));
}, { deep: true });



const total = computed(() => {
  return transactions.value.reduce((acc,transaction) => acc + transaction.amount,0)
})

const handleAddTransaction = (newTransaction) => {
    transactions.value.push({
        id: Date.now(), // or use a more robust ID generation
        ...newTransaction
    });
};

const handleDeleteTransaction = (id) => {
    transactions.value = transactions.value.filter(t => t.id !== id);
};



</script>

<template>
    
        <Header />
        <Balance :total="total" />
        <IncomeExpensis :transactions="transactions" />
        <div class="grid-container">

            <TransactionList :transactions="transactions" @delete-transaction="handleDeleteTransaction" />
            <AddTransaction :transactions="transactions"  @add-transaction="handleAddTransaction"/>
            
        </div>
</template>
  
