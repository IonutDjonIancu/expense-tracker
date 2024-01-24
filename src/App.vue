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
import { ref, onMounted } from "vue";
import TheHeader from "./components/TheHeader.vue";
import TheBalance from "./components/TheBalance.vue";
import IncomeExpenses from "./components/IncomeExpenses.vue";
import TransactionList from "./components/TransactionList.vue";
import AddTransaction from "./components/AddTransaction.vue";

const addTransaction = (data) => {
  transactions.value.push(data);

  storeTransactions();
};

const removeTransaction = (id) => {
  transactions.value = transactions.value.filter((t) => {
    return t.id != id;
  });

  storeTransactions();
};

const storeTransactions = () => {
  localStorage.setItem("transactions", JSON.stringify(transactions.value));
};

const transactions = ref([]);

onMounted(() => {
  const storedTransactions = JSON.parse(localStorage.getItem("transactions"));

  if (storedTransactions) {
    transactions.value = storedTransactions;
  }
});
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
