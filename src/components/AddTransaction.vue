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
        <br>
        <form @submit.prevent="addTransaction">
            <div class="form-controll">
                <!-- <label for="text">Text</label> -->
                <input 
                    v-model="newTransaction.text" 
                    type="text" 
                    id="text" 
                    placeholder="Enter text..."
                    required
                >
            </div>
            <br>
            <div class="form-controll">
                <!-- <label for="amount">
                    Amount 
                </label> -->
                <input 
                    v-model="newTransaction.amount" 
                    type="number" 
                    step="0.01"
                    id="amount" 
                    placeholder="Enter amount..."
                    required
                >
                <br>
                <button type="submit" class="btnn" >Add Transaction</button>
            </div>
        </form>
    </div>
 

</template>

