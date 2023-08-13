<template>
  <h1>9. Calculate the total annual income of the person by extracting the following text. 'He earns 5000 euro from salary per month, 10000 euro annual bonus, 15000 euro online courses per month.'</h1>
  <p>Annual income: {{ extract(text) }}</p>
  <p>Annual income (reduce method): {{ extractReduce(text) }}</p>
</template>

<script setup lang="ts">
const text = 'He earns 5000 euro from salary per month, 10000 euro annual bonus, 15000 euro online courses per month.'

function extract(str: string) {
  const sentences = str.split(',')
  let monthly = 0
  let annual = 0

  sentences.forEach(s => {
    if(s.match('per month')) return monthly += getMoney(s)
    if(s.match('annual')) annual += getMoney(s)
  })
  return annual + (12 * monthly)
}

function extractReduce(str: string) {
  const sentences = str.split(',')
  return sentences.reduce((acc: number, curr: string) => {
    if(curr.match('per month')) return acc + (12 * getMoney(curr))
    if(curr.match('annual')) return acc + getMoney(curr)
    return acc
  },0)
}

function getMoney(str: string): number {
  const n = str.match(/(\d+)/)
  if (n) return parseInt(n[0])
  return 0
}
</script>