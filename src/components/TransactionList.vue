<script setup>
import { computed } from 'vue';

const props = defineProps({
    transactions: {
        type: Array,
        required: true
    }
})

const emit = defineEmits(['delete-transaction']);

const deleteTransaction = (id) => {
    emit('delete-transaction', id);
    
};


const displayedTransactions = computed(() => props.transactions.slice(0, 3));


</script>

<template>
    <div class="transaction-list">

    
    <h3>History</h3>
    <ul id="list" class="list">

        
        <li v-for="transaction in displayedTransactions" :key="transaction.id" :class="transaction.amount > 0 ? 'plus' : 'minus' ">
            {{ transaction.text }} <span>{{ transaction.amount }}</span>
            <button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
        </li>
        <i class="arr pi pi-list-check" v-if="transactions.length == 0 "></i>
    </ul>
    <button v-if="transactions.length > 2" type="button" class="btnn" data-bs-toggle="modal" data-bs-target="#exampleModal" >View All</button>
    
</div>
       <!-- Modal -->

       <div class="modal  fade" id="exampleModal" tabindex="-1" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div class="modal-dialog modal-dialog-scrollable ">
                <div class="modal-content">
                    <div class="modal-header">
                        <h1 class="modal-title fs-5" id="exampleModalLabel">History Of Transactions</h1>
                        <button type="button" class="btn-close" data-bs-dismiss="modal" aria-label="Close"></button>
                    </div>
                    <div class="modal-body hihi">
                        
                        <ul id="list" class="list">

        <li v-for="transaction in transactions" :key="transaction.id" :class="transaction.amount > 0 ? 'plus' : 'minus' ">
        {{ transaction.text }} <span>{{ transaction.amount }}</span>
        <button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
        </li>
        </ul>
                    </div>
                    <div class="modal-footer">
                        <button type="button" class="btn btn-secondary" data-bs-dismiss="modal">Close</button>
                    </div>
                </div>
            </div>
        </div>

</template>

<style scoped>
.hihi {
    height: 1000px;
}

.arr {
    text-align: center;
    margin-top: 5%;
    margin-left: 8%;
    font-size: 180px;
}
</style>