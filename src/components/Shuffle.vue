<template>
  <h1>15. Write a function named shuffle, it takes an array parameter and it returns a shuffled array.</h1>
  <div class="example">
    <code><pre>
  shuffle([1,2,3,4,5]);
  [3,1,5,2,4]
    </pre></code>
  </div>
  <button @click="shuffle(result)">Shuffle</button>
  <p>{{ result }}</p>
</template>
<script setup lang="ts">
import { ref } from 'vue'

const result = ref<number[]>([1,2,3,4,5])

function shuffle(arr: number[]) {
  let currIndex = arr.length
  let randIndex

  while (currIndex != 0) {
    randIndex = Math.floor(Math.random() * currIndex)
    currIndex--
    [arr[currIndex], arr[randIndex]] = [arr[randIndex], arr[currIndex]]
  }
}
</script>