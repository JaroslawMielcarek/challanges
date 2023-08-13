<template>
  <Triangle/>
  <Replace/>
  <MaxOf3/>
  <Reverse/>
  <Modify/>
  <Random/>
  <NArguments/>
  <ReplaceWith/>
  <Interprate/>
  <CheckEnding/>
  <CountOccurance/>
  <CheckType/>
  <FilterGreaterThan/>
  <AvarageAge/>
  <Shuffle/>
  <FinishCarPlate/>
  <ShoppingCart/>
  <ToDoList/>
  <AreAllUnique/>
  <StudentsCollection/>
</template>

<script setup lang="ts">
import Triangle from './components/Triangle.vue'
import Replace from './components/Replace.vue'
import MaxOf3 from './components/MaxOf3.vue'
import Reverse from './components/Reverse.vue'
import Modify from './components/Modify.vue'
import Random from './components/Random.vue'
import NArguments from './components/NArguments.vue'
import ReplaceWith from './components/ReplaceWith.vue'
import Interprate from './components/Interprate.vue'
import CheckEnding from './components/CheckEnding.vue'
import CountOccurance from './components/CountOccurance.vue'
import CheckType from './components/CheckType.vue'
import FilterGreaterThan from './components/FilterGreaterThan.vue'
import AvarageAge from './components/AvarageAge.vue'
import Shuffle from './components/Shuffle.vue'
import FinishCarPlate from './components/FinishCarPlate.vue'
import ShoppingCart from './components/ShoppingCart.vue'
import ToDoList from './components/ToDoList.vue'
import AreAllUnique from './components/AreAllUnique.vue'
import StudentsCollection from './components/StudentsCollection.vue'

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
}
label { margin-top: 6px; margin-right: 1ch; }
button { margin-top: 12px; }
.flex-column{
  display: flex;
  flex-direction: column;
}
.example {
  font-weight: lighter;
  font-style: italic;
  color:cadetblue;
  &::before {
    content: 'Examples: ';
    width: 10ch;
    display: block;
  }
  p {
    margin: 0.1em 0;
  }
}
.extra-message {
  font-size: 0.9em;
  font-weight: lighter;
}
.required {
  &::after{
    content: '*';
    vertical-align: super;
    font-size: smaller;
    font-weight: lighter;
  }
}
.close {
  position: absolute;
  right: 12px;
  top: 12px;
  width: 16px;
  height: 16px;
  opacity: 0.3;
}
.close:hover {
  opacity: 1;
}
.close:before, .close:after {
  position: absolute;
  left: 6px;
  content: ' ';
  height: 16px;
  width: 2px;
  background-color: #333;
}
.close:before {
  transform: rotate(45deg);
}
.close:after {
  transform: rotate(-45deg);
}
</style>
