<template>
  <div>
    <h4>add new transaction</h4>
    <form @submit.prevent="submitForm" id="form">
      <div>
        <label for="text">text</label>
        <input v-model="text" type="text" id="text" />
      </div>
      <div>
        <label for="amount"> amount </label>
        <input v-model="amount" type="text" id="amount" />
      </div>
      <button type="submit">add transaction</button>
    </form>
  </div>
</template>

<script setup>
import { ref, defineEmits } from "vue";

const emit = defineEmits(["on-submit"]);

const text = ref("");
const amount = ref("");

const submitForm = () => {
  const data = {
    id: Math.floor(Math.random() * 1000000),
    text: text.value,
    amount: parseFloat(amount.value),
  };

  emit("on-submit", data);

  text.value = "";
  amount.value = "";
};
</script>
