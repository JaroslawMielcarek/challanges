<template>
<h1>2. FizzBuzz Write a program that uses console.log to print all the numbers from 1 to 100, with two exceptions. For numbers divisible by 3, print "Fizz" instead of the number, and for numbers divisible by 5 (and not 3), print "Buzz" instead. When you have that working, modify your program to print "FizzBuzz" for numbers that are divisible by both 3 and 5 (and still print "Fizz" or "Buzz"for numbers divisible by only one of those).</h1>
<p>a. fizz || buzz:</p>
<div class="grid-temp">
  <span v-for="e in fizzbuzz(ar)" :key="e">{{ e }}</span>
</div>
<p>b. fizz & Buzz:</p>
<div class="grid-temp">
  <span v-for="e in fizzBuzz2(ar)" :key="e">{{ e }}</span>
</div>
</template>

<script setup lang="ts">
const ar = Array.from(Array(101).keys()).slice(1)

function fizzbuzz(arr: number[]): string[] {
  return arr.map((e: number) => {
    if (!(e % 3) && (e % 5)) return 'Fizz'
    if (!(e % 5) && (e % 3)) return 'Buzz'
    return e.toString()
  })
}

function fizzBuzz2(arr: number[]): string[] {
  return arr.map((e: number) => {
    if (!(e % 3) && !(e % 5)) return 'FizzBuzz'
    if (!(e % 3)) return 'Fizz'
    if (!(e % 5)) return 'Buzz'
    return e.toString()
  })
}
</script>
<style>
.grid-temp { display: grid; grid-template-columns: repeat(10, 7ch);}
</style>