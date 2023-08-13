<template>
<h1>3. Maximum Math.max returns its largest argument. We can build something like that now. Write a function findMax that takes three arguments and returns their maxiumum. Without method Math.max method.</h1>
<p>a. {{ arr1 }} - max: {{ findMax(arr1)  }} - max(reduce): {{ findMaxReduce(arr1) }} </p>
<p>b. {{ arr2 }} - max: {{ findMax(arr2)  }} - max(reduce): {{ findMaxReduce(arr2) }} </p>
</template>

<script setup lang="ts">
const arr1 = [0, 10, 5]
const arr2 = [0, -10, -2]

function findMax(arr: number[]) {
  const [a,b,c] = arr
  let max = a
  if (b > max) max = b
  if (c > max) max = c
  return max
}
function findMaxReduce(arr: number[]) {
  return arr.reduce((acc, curr) => {
    if (curr > acc) acc = curr
    return acc
  },0)
}
</script>