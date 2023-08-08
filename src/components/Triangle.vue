<template>
<h1>1. Looping a triangle Write a loop that output the following triangle:</h1>
{{ ejemplo }}
<h2>1.1 solution</h2>
  <p>a. while loop</p>
  <p>{{ triangleSimple }}</p>
  <p>{{ triangleSimple() }}</p>
  <p>b. reduce</p>
  {{ triangleReduce() }}
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
  const ar = Array.from(Array(7).keys())
  return ar.reduce((acc, curr, index) => {
    acc += '#'.repeat(index + 1) + '\n'
    return acc
  },'')
}
</script>