<template>
  <h1>16. Write a function which can generate a random Finnish car code.</h1>
  <p><pre>
    Regular, non-vanity plates also have some more limitations:
    2-3 letters & 1-3 numbers (5 in Åland)
    The letters used are A-Z and Å, Ä & Ö
    The letter part may not begin with P, W or D (used for trailers, but if you want to buy a specific plate then you can have also these letters in the beginning)
    The number part may not begin with 0
  </pre></p>
  <div class="example">
    <code><pre>
  console.log(genCarPlateNum())
  AFG-205
  console.log(genCarPlateNum())
  JCB-586
    </pre></code>
  </div>
  <button @click="generatePlate()">Generate</button>
  <p>{{ plate }}</p>
</template>
<script setup lang="ts">
import { onMounted, ref } from 'vue'

const CHARACTERS ='ABCDEFGHIJKLMNOPQRSTUVWXYZÅÄÖ'
const PROHIBITED_FIRST_LETTERS = ['P','W','D']

const plate = ref<string>('')
const numbers = Array.from(Array(10).keys())

onMounted(() => generatePlate())

function generatePlate(){
  plate.value = getRandomString(CHARACTERS.split(''), getRandomFromRange(2, 3)) +'-'+ getRandomString(numbers, getRandomFromRange(1, 3))
}

function getRandomFromRange(min: number, max: number) {
  return Math.floor(Math.random() * (max - min + 1)) + min
}
function getRandomString(range: any[], length: number) {
  let result = ''
  for (let i = 1; i <= length; i++){
    const c = range[Math.floor(Math.random() * range.length)]
    if ((typeof c === 'string' && i === 1 && PROHIBITED_FIRST_LETTERS.includes(c)) || (typeof c === 'number' && i === 1 && !c)) return i--
    result += c
  }
  return result
}
</script>