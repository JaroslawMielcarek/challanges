<template>
  <Triangle/>
  <Replace/>
</template>

<script setup lang="ts">
import Triangle from './components/Triangle.vue'
import Replace from './components/Replace.vue'


function ran(){
  const ar = []
  while(ar.length < 7){
    const r = Math.floor(Math.random() * 9)
    if (ar.indexOf(r) === -1) ar.push(r)
  }
  return ar
}
const ar = [1,2,3,4,5]
const msg = adaptive()
function adaptive() {
  const arg = Array.from(arguments)
  return arg.reduce((acum, curr) => {
    acum += curr
    return acum
  }, 0)
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
  white-space: pre-wrap;
}
</style>
