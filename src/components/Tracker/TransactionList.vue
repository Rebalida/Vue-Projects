<template>
    <h3>History</h3>
    
    <ul id="list" class="list">
        <li 
            v-for="transaction in transactions"
            :key="transaction.id"
            :class="transaction.amount < 0 ? 'minus' : 'plus'"
        >
            {{ transaction.text }} <span>₱ {{ transaction.amount }}</span>
            <button @click="deleteTransaction(transaction.id)" class="delete-btn">x</button>
        </li>
    </ul>
</template>

<script setup>

    import { defineProps, defineEmits } from 'vue';

    const emit = defineEmits(['transactionDeleted']);

    const props = defineProps({
        transactions: Array,
        required: true
    })

    const deleteTransaction = (id) => {
        emit('transactionDeleted', id)
    }

</script>

<style scoped>

h3 {
    border-bottom: 1px solid #bbb;
    padding-bottom: 10px;
    margin: 40px 0 10px;
    color: #f0f0f0;
}

.list {
    list-style-type: none;
    padding: 0;
    margin-bottom: 40px;
}

.list li {
    background-color: #fff;
    box-shadow:  0 2px 4px rgba(0, 0, 0, 0.1);
    color: #333;
    display: flex;
    justify-content: space-between;
    position: relative;
    padding: 10px;
    margin: 10px 0;
}

.list li.plus {
    border-right: 5px solid #2ecc71;
}

.list li.minus {
    border-right: 5px solid #c0392b;
}

.delete-btn {
    cursor: pointer;
    background-color: #e74c3c;
    border: 0;
    color: #fff;
    font-size: 20px;
    line-height: 20px;
    padding: 2px 5px;
    position: absolute;
    top: 50%;
    left: 0;
    transform: translate(-100%, -50%);
    opacity: 0;
    transition: opacity 0.3s ease;
}

.list li:hover .delete-btn {
    opacity: 1;
}

</style>
