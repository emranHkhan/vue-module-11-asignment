<script setup>
import { ref } from 'vue'
const symbols = ['+', '-', 'x', '/', '0', '1', '2', '3', '4', '5', '6', '7', '8', '9', '=', 'CE']
const left = ref("")
const operator = ref(null)
const right = ref("")
const ans = ref('')
const isLeftInputFocused = ref(false)

const handleBtnClick = (symbol) => {
  if ('+-/x'.includes(symbol)) {
    operator.value = symbol
  } else if (symbol === '=') {
    if (operator.value === '+') ans.value = parseInt(left.value) + parseInt(right.value)
    if (operator.value === '-') ans.value = parseInt(left.value) - parseInt(right.value)
    if (operator.value === '/') ans.value = parseInt(left.value) / parseInt(right.value)
    if (operator.value === 'x') ans.value = parseInt(left.value) * parseInt(right.value)
    isLeftInputFocused.value = false
  } else if (symbol === 'CE') {
    left.value = ''
    right.value = ''
    operator.value = ''
    ans.value = ''
  }
  else {
    if (operator.value) {
      right.value += symbol
    } else {
      left.value += symbol
    }
  }
}

</script>

<template>
  <div class="bg-white py-2 px-3 rounded-lg shadow-xl border-2 border-lime-500">
    <p class="text-lime-500 font-semibold text-center pb-2 uppercase">Calculator</p>
    <div class="flex flex-col">
      <input type="number"
        class="number-input border-2 border-lime-500 focus:border-lime-500 focus:outline-none text-right px-1"
        v-model="left" @focus="isLeftInputFocused = true">

      <input type="text"
        class="px-1 border-2 border-lime-500 focus:border-lime-500 focus:outline-none self-center my-1 text-center font-bold placeholder:text-slate-300 cursor-pointer"
        v-model="operator" readonly placeholder="+">

      <input type="number"
        class="number-input border-2 border-lime-500 focus:border-lime-500 focus:outline-none text-right px-1"
        v-model="right" :disabled="left.length != 0 && operator !== null ? false : true">
    </div>

    <div
      class="rounded-sm font-semibold text-white p-1 mt-1 text-center cursor-pointer transition ease-in-out delay-100 shadow-md"
      :class="ans ? 'bg-lime-500' : 'bg-slate-300'">{{ ans ? ans :
        'Answer' }}</div>

    <div class="grid grid-cols-3 gap-4 mt-5 pb-2">
      <div v-for="(symbol, index) in symbols" :key="index"
        class="text-center border-2 border-lime-500 text-lime-500 cursor-pointer hover:bg-lime-500 hover:text-white hover:font-semibold rounded-lg font-semibold transition duration-300 ease-in-out transform shadow-md active:scale-75"
        :class="isLeftInputFocused && 'x-+/'.includes(symbol) ? 'bg-lime-500 text-white' : ''"
        @click="handleBtnClick(symbol)">
        {{
          symbol }}</div>
    </div>

  </div>
</template>

<style scoped>
.number-input::-webkit-inner-spin-button,
.number-input::-webkit-outer-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>
