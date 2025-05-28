<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'
import { useToast } from 'vue-toastification'
import { ref, computed } from 'vue'

const toast = useToast()

const transactions = ref([
  { id: 1, text: 'Sandals', amount: -19.99 },
  { id: 2, text: 'Books', amount: +14.99 },
  { id: 3, text: 'AirPods', amount: -79.99 },
  { id: 4, text: 'Tea', amount: +0.99 },
])

const total = computed(() => {
  return transactions.value.reduce((acc, transaction) => {
    return acc + transaction.amount
  }, 0)
})

const income = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount > 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

const expenses = computed(() => {
  return transactions.value
    .filter((transaction) => transaction.amount < 0)
    .reduce((acc, transaction) => {
      return acc + transaction.amount
    }, 0)
    .toFixed(2)
})

const handleTransactionSubmitted = (transactionData) => {
  transactions.value.push({
    id: generateID(),
    text: transactionData.text,
    amount: transactionData.amount,
  })
  toast.success('Transaction Added')
}

const generateID = () => {
  return Math.floor(Math.random() * 1000000)
}

const handleTransactionDeleted = (id) => {
  transactions.value = transactions.value.filter((transaction) => transaction.id !== id)
  toast.success('Transaction Deleted')
}
</script>

<template>
  <Header />
  <div class="container">
    <Balance :total="+total" />
  </div>
  <IncomeExpenses :income="+income" :expenses="+expenses" />
  <TransactionList :transactions="transactions" @transactionDeleted="handleTransactionDeleted" />
  <AddTransaction @transactionSubmitted="handleTransactionSubmitted" />
</template>
