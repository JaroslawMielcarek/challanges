<template>
<h1>1. Looping a triangle Write a loop that output the following triangle:</h1>
<p class="example">{{ ejemplo }}</p>
<h2>1.1 solution</h2>
  <label>a. while loop</label>
  <p>{{ triangleSimple() }}</p>
  <label>b. reduce</label>
  <p>{{ triangleReduce() }}</p>
</template>

<script setup lang="ts">
const ejemplo = `
#
##
###
####
#####
######
#######`
function triangleSimple(){
  let str = ''
  for(let x = 1; x<=7;x++){
    str += '#'.repeat(x) + '\n'
  }
  return str
}
function triangleReduce(){
  return Array.from(Array(7).keys()).reduce((acc, curr, index) => acc + '#'.repeat(index + 1) + '\n','')
}
</script>
<style scoped>
p { white-space: pre-wrap; }
</style>