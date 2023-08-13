<template>
  <h1>8. Write a function which removes items from the middle of an array and replace with three items.</h1>
  <div class="example">
    <p>removeMiddleItem([1,2,3], 4,5,6) [1,4,5,6,3]</p>
    <p>removeMiddleItem([1,2,3,4], 4,5,6) [1,4,5,6,4]</p>
  </div>
  <h3>1.</h3>
  <p>Array: {{ arr1 }}, Insert: {{ rep }}</p>
  <p>Result: {{ removeMiddleItem([...arr1], rep) }}</p>
  <h3>2.</h3>
  <p>Array: {{ arr2 }}, Insert: {{ rep }}</p>
  <p>Result: {{ removeMiddleItem([...arr2], rep) }}</p>
</template>
<script setup lang="ts">
const arr1 = [1,2,3]
const arr2 = [1,2,3,4]
const rep = [4,5,6]

function removeMiddleItem(arr: number[], rep: number[]) {
  return [arr.shift(), ...rep, arr.pop()]
}
</script>