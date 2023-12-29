<script setup>
import {ref} from "vue";
import {useToast} from "vue-toastification";

const text = ref("");
const amount = ref("");

const emit = defineEmits(["addTransaction"]);

const toast = useToast();

const onsubmit = () => {
  if (text.value === "" || amount.value === "") {
    toast.error('Both fields are required')
  } else {
    const newTransaction = {
      id: Math.floor(Math.random() * 100000000),
      text: text.value,
      amount: +amount.value,
    };
    emit("addTransaction", newTransaction);

    text.value = "";
    amount.value = "";
  }
};
</script>

<template>
  <h3>Add new transaction</h3>
  <form id="form" @submit.prevent="onsubmit">
    <div class="form-control">
      <label for="text">Text</label>
      <input type="text" id="text" v-model="text" placeholder="Enter text..." />
    </div>
    <div class="form-control">
      <label for="amount"
      >Amount <br />
        (negative - expense, positive - income)</label
      >
      <input type="text" id="amount" v-model="amount" placeholder="Enter amount..." />
    </div>
    <button class="btn">Add transaction</button>
  </form>
</template>

<style scoped>

</style>