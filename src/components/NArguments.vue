<template>
  <h1>7. Write a funch which takes any number of arguments and return the sum of the arguments</h1>
  <div class="example">
    <p>sum(1,2,3) 6</p>
    <p>sum(1,2,3,4) 10</p>
  </div>
  <select v-model="selectedNr">
    <option v-for="x of options" :key="x">{{ x }}</option>
  </select>
  <p>Permit dupplicated arguments: <input type="checkbox" v-model="dupplicated"></p>
  <p>Arguments: {{ args }}</p>
  <p>Sum: {{ result }}</p>
</template>

<script setup lang="ts">
import { ref, computed } from 'vue'

const dupplicated = ref<boolean>(false)
const selectedNr = ref<number>(1)
const options = Array.from(Array(11).keys()).slice(1)

const args = computed(() => generateArg(selectedNr.value))
const result = computed(() => nArg(...args.value))

function generateArg(nr: number) {
  const arr: number[] = []
  while (arr.length < nr) {
    const r = Math.floor(Math.random() * 20)
    if (!dupplicated.value && arr.includes(r)) continue
    arr.push(r)
  }
  return arr
}

function nArg(...arg: number[]) {
  return arg.reduce((acc, curr) => acc + curr,0)
}
</script>