<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const toast = useToast()

// Define a prop to receive and emit transaction updates
const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
});

// Emit event to parent for adding transactions
const emit = defineEmits(['add-transaction']);

// Local reactive state for new transaction
const newTransaction = ref({
    text: '',
    amount: null
});

// Add transaction method
const addTransaction = () => {
    // Validate inputs
    if (!newTransaction.value.text || !newTransaction.value.amount) {
        alert('Please enter text and amount');
        return;
    }

    // Emit event to parent component to add transaction
    emit('add-transaction', {
        text: newTransaction.value.text,
        amount: Number(newTransaction.value.amount)
    });

    // Reset form
    newTransaction.value.text = '';
    newTransaction.value.amount = null;
    toast.success('Transaction Added Succesfully');
};




</script>

<template>
    <div class="add-transaction">
        <h3>Add new Transaction</h3>
        <form @submit.prevent="addTransaction">
            <div class="form-control">
                <label for="text">Text</label>
                <input 
                    v-model="newTransaction.text" 
                    type="text" 
                    id="text" 
                    placeholder="Enter text..."
                    required
                >
            </div>
            <div class="form-control">
                <label for="amount">
                    Amount 
                </label>
                <input 
                    v-model.number="newTransaction.amount" 
                    type="number" 
                    id="amount" 
                    placeholder="Enter amount..."
                    required
                >
                <button type="submit" class="btn">Add Transaction</button>
            </div>
        </form>
    </div>
</template>