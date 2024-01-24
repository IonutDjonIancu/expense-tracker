<template>
  <div>
    <h3>history</h3>
    <ul id="list">
      <li :key="tran.id" v-for="tran in props.transactions">
        {{ tran.text }} <span>${{ tran.amount }} | </span>
        <span
          @click="onRemove(tran.id)"
          :class="tran.amount > 0 ? 'remove plus' : 'remove minus'"
        >
          x |</span
        >
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps, defineEmits } from "vue";

const props = defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(["on-remove-transaction"]);

const onRemove = (id) => {
  emit("on-remove-transaction", id);
};
</script>

<style scoped>
.plus {
  border-left-width: 5px;
  border-left-color: green;
  border-left-style: solid;
}
.minus {
  border-left-width: 5px;
  border-left-color: rgb(177, 40, 40);
  border-left-style: solid;
}

.remove {
  cursor: pointer;
}
</style>
