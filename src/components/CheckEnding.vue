<template>
  <h1>10. Create a function that takes two strings and returns true if the first argument ends with the second argument; otherewise return false . Take two strings as arguments. Determine if second string matches ending of first string. Return boolean value. Example</h1>
  <div class="example">
    <p>yourFunc("integrity", "ity") true</p>
    <p>yourFunc("integration", "tio") false</p>
    <p>yourFunc("connection", "sion") false</p>
    <p>yourFunc("connection", "tion") true</p>
  </div>
  <p>"integrity", "ity": {{ checkEnd("integrity", "ity") }}</p>
  <p>"integration", "tio": {{ checkEnd("integration", "tio") }}</p>
  <p>"connection", "sion": {{ checkEnd("connection", "sion") }}</p>
  <p>"connection", "tion": {{ checkEnd("connection", "tion") }}</p>
</template>

<script setup lang="ts">

function checkEnd(str: string, end: string) {
  return RegExp(end + '$').test(str)
}
</script>