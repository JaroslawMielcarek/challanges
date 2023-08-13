<template>
  <h1>14. Write a function which calculate the average age of the group.</h1>
  <div class="example">
    <code><pre>
  console.log(averageAge(ages));
  22
    </pre></code>
  </div>
  <p>{{ avarageAge(group) }}</p>
</template>
<script setup lang="ts">
const group = [35, 30, 17, 18, 15, 22, 16, 20]

function avarageAge(arr: number[]){
  const av = arr.reduce((acc, curr) => acc + curr, 0)
  return Math.round(av/arr.length)
}
</script>