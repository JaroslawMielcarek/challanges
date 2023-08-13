<template>
  <h1>12. Write a function which takes an array parameter and returns an array of the data types of each item:</h1>
  <div class="example">
    <code><pre>
const arr = ['Asabeneh', 100, true, null, undefined, {job:'teaching'}];
console.log(checkDatatTypes(arr));
["string", "number", "boolean", "object", "undefined", "object"]

const mixedData = ["John", 25, "David", 30, "Sara", 22];
console.log(checkDatatTypes(mixedData));
["string","number","string","number","string","number"];
    </pre>
    </code>
  </div>
  <p>{{ checkDatatTypes(arr1) }}</p>
  <p>{{ checkDatatTypes(arr2) }}</p>
</template>

<script setup lang="ts">
const arr1 = ['Asabeneh', 100, true, null, undefined, {job:'teaching'}]
const arr2 = ["John", 25, "David", 30, "Sara", 22]

function checkDatatTypes(arr: any) {
  return arr.map((e: any) => typeof e)
}
</script>