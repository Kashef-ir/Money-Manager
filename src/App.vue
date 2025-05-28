<script setup>
import Header from './components/Header.vue'
import Balance from './components/Balance.vue'
import IncomeExpenses from './components/IncomeExpenses.vue'
import TransactionList from './components/TransactionList.vue'
import AddTransaction from './components/AddTransaction.vue'

import { ref } from 'vue'

const transactions = ref([
  { id: 1, text: 'Sandals', amount: -19.99 },
  { id: 2, text: 'Books', amount: +14.99 },
  { id: 3, text: 'AirPods', amount: -79.99 },
  { id: 4, text: 'Tea', amount: +0.99 },
])
</script>

<template>
  <Header />
  <div class="container">
    <Balance />
  </div>
  <IncomeExpenses />
  <TransactionList :transactions="transactions" />
  <AddTransaction />
</template>
