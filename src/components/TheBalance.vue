<template>
  <div>
    <h4>your balance</h4>
    <h2 id="balance">${{ balance }}</h2>
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
let balance = computed(() => {
  return props.transactions.reduce((acc, tran) => {
    return acc + tran.amount;
  }, 0);
});
</script>

<style></style>
