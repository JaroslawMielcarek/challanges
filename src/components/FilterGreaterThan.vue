<template>
  <h1>13. Create a function which filter ages greater than 18.</h1>
  <div class="example">
    <code><pre>
  const ages = [35, 30, 17, 18, 15, 22, 16, 20];
  console.log(agesGreaterEighteen(ages));
  [35, 30, 22, , 20];
    </pre></code>
  </div>
  <p>{{ filterGreater([35, 30, 17, 18, 15, 22, 16, 20], 18) }}</p>
</template>
<script setup lang="ts">

function filterGreater(arr: number[], limit: number) {
  return arr.filter(e => e > limit)
}
</script>