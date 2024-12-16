<template>
  <main>
    <h1>Expense Tracker</h1>
    <div class="container">
      <Balance :total="+total"/>
      <IncomeExpenses :income="+income" :expenses="+expenses"/>
      <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted"/>
      <AddTransaction @transactionSubmitted="handleTransactionSubmitted"/>
    </div>
  </main>
</template>

<script setup>

  import Balance from '@/components/Tracker/Balance.vue';
  import IncomeExpenses from '@/components/Tracker/IncomeExpenses.vue';
  import TransactionList from '@/components/Tracker/TransactionList.vue';
  import AddTransaction from '@/components/Tracker/AddTransaction.vue';
  import { uid } from 'uid';

  import {useToast} from 'vue-toastification';

  import { ref, computed, onMounted, watch } from 'vue';

  const toast = useToast();

  const transactions = ref ([]);


  onMounted(() => {
    const savedTransactions = JSON.parse(localStorage.getItem('transactions'));

    if(savedTransactions) {
      transactions.value = savedTransactions;
    }
  })

  //Get Balance
  const total = computed (() => {
    return transactions.value.reduce((acc, transaction) => {
      return acc + transaction.amount;
    }, 0)
  });

  //Get Income
  const income = computed (() => {
    return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});


  //Get Expenses
  const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => acc + transaction.amount, 0)
    .toFixed(2);
});

  //Add Transaction
  const handleTransactionSubmitted = (transactionData) => {
    transactions.value.push({
      id: uid(),
      text: transactionData.text,
      amount: transactionData.amount,
    });

    saveTransactionToLocalStorage();
    toast.success('Transaction Added');
  }

  //Generate Unique ID
  const generateUniqueId = () => {
  return Math.floor(Math.random() * 1000000);
};

  //Delete Transaction
  const handleTransactionDeleted = (id) => {
    transactions.value = transactions.value.filter((transaction) => 
      transaction.id !== id);

      saveTransactionToLocalStorage();
      toast.success('Transaction Deleted')

  }

  //Save Local
  const saveTransactionToLocalStorage = () => {
    localStorage.setItem('transactions', JSON.stringify(transactions.value));
  }

</script>

<style scoped>

main {
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    margin: 0;
    padding: 40px 15px;
    font-size: 18px;
}

.container {
    margin: 30px auto;
    width: 400px;
}

h1 {
    letter-spacing: 1px;
    margin: 0;
}

</style>
