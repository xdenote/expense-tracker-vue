<script setup>
import {  defineProps } from 'vue'

const props = defineProps({
  total: {
    type: String,
    required: true
  }
})

</script>

<template>
  <h4>Your Balance</h4>
  <h1 id="balance">${{total}}</h1>
</template>

<style scoped>

</style>