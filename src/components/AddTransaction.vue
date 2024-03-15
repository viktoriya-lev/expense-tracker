<template>
  <h3>Add New Transaction</h3>
  <form @submit.prevent="onSubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input
        v-model="text"
        id="text"
        type="text"
        placeholder="Enter text..."
      />
    </div>
    <div class="form-control">
      <label for="amount">
        Amount
        <br />
        (negative - expense, positive - income)
      </label>
      <input
        v-model="amount"
        id="amount"
        type="number"
        placeholder="Enter amount..."
      />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<script setup>
import { ref } from 'vue';
import { useToast } from 'vue-toastification';

const text = ref('');
const amount = ref('');

const emit = defineEmits(['transaction-submitted']);

const toast = useToast();
const onSubmit = () => {
  if (!text.value || !amount.value) {
    toast.error('Both fields must be filled');
    return;
  }

  const transactionData = {
    text: text.value,
    amount: parseFloat(amount.value),
  }

  emit('transaction-submitted', transactionData);

  text.value = '';
  amount.value = '';
}
</script>
