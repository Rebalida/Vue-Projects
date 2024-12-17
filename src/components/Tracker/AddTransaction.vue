<template>
    <h3>Add new transaction</h3>
    <form id="form" @submit.prevent="onSubmit">
        <div class="form-control">
            <label for="text">Text</label>
            <input type="text" id="text" v-model="text"
            placeholder="Enter text...">
        </div>
        <div class="form-control">
            <label for="amount">Amount <br>
                (negative - expense, positive - income)
            </label>
            <input type="text" id="amount" v-model="amount" placeholder="Enter amount...">
        </div>
        <button class="btn">Add transaction</button>
    </form>
</template>

<script setup>

    import { ref } from 'vue';
    import {useToast} from 'vue-toastification';

    const text = ref('');
    const amount = ref('');

    const emit = defineEmits(['transactionSubmitted']);

    const toast = useToast();

    const onSubmit = () => {
        if(!text.value || !amount.value){
            toast.error('Both fields must be filled');
            return;
        }
        
        const transactionData = {
            text: text.value,
            amount: parseFloat(amount.value),
        }

        emit('transactionSubmitted', transactionData);

        text.value = '';
        amount.value ='';
    }

</script>

<style scoped>

h3 {
    border-bottom: 1px solid #bbb;
    padding-bottom: 10px;
    margin: 40px 0 10px;
    color: #f0f0f0;
}

.form-control {
    margin: 10px 0;
    border-radius: 0;
}

label {
    display: inline-block;
    margin: 10px 0;
}

input[type='text'],
input[type='number'] {
    border: 1px solid #dedede;
    display: block;
    font-size: 16px;
    padding: 10px;
    width: 100%;
}

.btn {
    cursor: pointer;
    background-color: #4DBA87;
    color: #fff;
    border: 0;
    border-radius: 0;
    display: block;
    font-size: 16px;
    margin: 10px 0 30px;
    padding: 10px;
    width: 100%;
}

.btn:focus {
    outline: 0;
}

</style>
