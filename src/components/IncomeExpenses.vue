<template>
  <div>
    <h4>Income</h4>
    <p id="money-plus">$ {{ income }}</p>
    <h4>Expense</h4>
    <p id="money-minus">$ {{ expense }}</p>
  </div>
</template>

<script setup>
import { defineProps, computed } from "vue";

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

let income = computed(() => {
  return props.transactions
    .filter((tran) => {
      return tran.amount > 0;
    })
    .reduce((acc, tran) => {
      return acc + tran.amount;
    }, 0)
    .toFixed(2);
});

let expense = computed(() => {
  return props.transactions
    .filter((tran) => {
      return tran.amount < 0;
    })
    .reduce((acc, tran) => {
      return acc + tran.amount;
    }, 0)
    .toFixed(2);
});
</script>

<style></style>
