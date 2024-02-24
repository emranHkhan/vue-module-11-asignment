<script setup>
import Calculator from './components/Calculator.vue'
import FetchData from './components/FetchData.vue';
import { ref } from 'vue'

const isCalculatorVisible = ref(true)
const isDataVisible = ref(false)

</script>

<template>
  <div class="mb-5">
    <button
      class="text-lime-500 py-1 px-2 font-semibold border-2 border-lime-500 rounded-md hover:bg-lime-500 hover:text-white"
      @click="isCalculatorVisible = true; isDataVisible = false"
      :class="isCalculatorVisible ? 'bg-lime-500 text-white' : ''">Calculator</button>
    <button
      class="text-lime-500 py-1 px-2 font-semibold border-2 border-lime-500 rounded-md hover:bg-lime-500 hover:text-white ml-2"
      @click="isCalculatorVisible = false; isDataVisible = true"
      :class="isDataVisible ? 'bg-lime-500 text-white' : ''">API
      data</button>
  </div>
  <Calculator v-show="isCalculatorVisible" />
  <FetchData v-show="isDataVisible" />
</template>

<style scoped></style>
