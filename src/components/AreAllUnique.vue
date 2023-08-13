<template>
  <h1>19. Write a function which check if items of an array are unique?</h1>
  <div class="example">
    <code><pre>
  const arrOne = [1, 4, 6, 2, 1];
  console.log(checkUniqueness(arrOne));
  false
  const arrTwo = [1, 4, 6, 2, 3]
  console.log(checkUniqueness(arrTwo));
  true
    </pre></code>
  </div>
  <p>{{ arr1 }}</p>
  <p>{{ allUnique(arr1) }}</p>

  <p>{{ arr2 }}</p>
  <p>{{ allUnique(arr2) }}</p>
</template>
<script setup lang="ts">
const arr1 = [1, 4, 6, 2, 1]
const arr2 = [1, 4, 6, 2, 3]

const allUnique = (arr: number[]) => (new Set(arr)).size === arr.length
</script>