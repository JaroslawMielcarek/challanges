<template>
<h1>4. Reversing an array Arrays have a reverse method which changes the array by inverting the order in which its elements appear. For this exercise, write a function, reverseArray. The reverseArray, takes an array as argument and produces a new array that has the same elements in the inverse order. Without reverse method.</h1>
<p>{{ arr }}</p>
<label>a. Reduce</label>
<p>{{ reverseArrayReduce(arr) }}</p>
<label>b. Map</label>
<p>{{ reverseArrayMap(arr) }}</p>
</template>

<script setup lang="ts">
const arr = ["C", "B", "A"]

function reverseArrayReduce(arr: string[]) {
  return arr.reduce((acc: string[], curr: string)=> {
    acc.unshift(curr)
    return acc 
  },[])
}
function reverseArrayMap(arr: string[]) {
  const ar: string[] = []
  arr.map(e => ar.unshift(e))
  return ar
}
</script>