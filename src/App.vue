<template>
  <div class="app">
    <TheHeader></TheHeader>
    <TheBalance :transactions="transactions"></TheBalance>
    <IncomeExpenses :transactions="transactions"></IncomeExpenses>
    <TransactionList
      @on-remove-transaction="removeTransaction"
      :transactions="transactions"
    ></TransactionList>
    <AddTransaction @on-submit="addTransaction"></AddTransaction>
  </div>
</template>

<script setup>
import { ref } from "vue";
import TheHeader from "./components/TheHeader.vue";
import TheBalance from "./components/TheBalance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

const addTransaction = (data) => {
  transactions.value.push(data);
};

const removeTransaction = (id) => {
  transactions.value = transactions.value.filter((t) => {
    return t.id != id;
  });
};

const transactions = ref([
  {
    id: Math.floor(Math.random() * 1000000),
    text: "flowers",
    amount: -10,
  },
  {
    id: Math.floor(Math.random() * 1000000),
    text: "salary",
    amount: 7000,
  },
  {
    id: Math.floor(Math.random() * 1000000),
    text: "trip",
    amount: -4000,
  },
]);
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
