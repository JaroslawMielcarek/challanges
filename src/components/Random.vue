<template>
  <h1>6. Write a function which returns array of seven random numbers in a range of 0-9. All the numbers must be unique</h1>
  <div class="example">
    <p>sevenRandomNumbers() [1,4,5,7,9,8,0]</p>
  </div>
  <p>{{ ran }}</p>
  <button @click="ran = random()">Generate</button>
</template>

<script setup lang="ts">
import { onMounted, ref } from 'vue'
let ran = ref<number[]>([])

onMounted(() => ran.value = random())

function random(){
  const ar: number[] = []
  while (ar.length <= 7) {
    const r = Math.floor(Math.random() * 9 )
    if (!ar.includes(r)) ar.push(r)
  }
  return ar
}
</script>