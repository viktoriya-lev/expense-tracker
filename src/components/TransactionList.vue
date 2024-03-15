<template>
  <h3>History</h3>
  <ul class="list">
    <li
      v-for="transaction in transactions"
      :key="`key-${transaction.id}`"
      :class="transaction.amount < 0 ? 'minus' : 'plus'"
    >
      {{ transaction.text }}
      <span>
        ${{ transaction.amount }}
      </span>
      <button
        @click="deleteTransaction(transaction.id)"
        class="delete-btn"
      >
        x
      </button>
    </li>
  </ul>

</template>

<script setup>
defineProps({
  transactions: {
    type: Array,
    required: true,
  },
});

const emit = defineEmits(['transaction-deleted']);

const deleteTransaction = (id) => {
  emit('transaction-deleted', id)
};
</script>
