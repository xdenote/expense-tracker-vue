<script>
import Header from "@/components/Header.vue";
import {defineComponent} from "vue";
import Balance from "@/components/Balance.vue";
import IncomeExpenses from "@/components/IncomeExpenses.vue";
import TransactionList from "@/components/TransactionList.vue";
import AddTransactions from "@/components/AddTransactions.vue";

export default defineComponent({
  components: {AddTransactions, TransactionList, IncomeExpenses, Balance, Header}
})


</script>

<template>
  <Header/>
  <div class="container">
    <Balance/>
    <IncomeExpenses/>
    <TransactionList/>
    <AddTransactions/>
  </div>
</template>