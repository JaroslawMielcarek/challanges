<template>
  <h1>5. Modifying an array Write a function called modifyArray takes array as parameter and modifies the fifth item of the array and returns the array. If the array length is less than five it return ‘item not found’.</h1>
  <p>Map method:</p>
  <p>{{ arr1 }}</p>
  <p>{{ modifyArray(arr1) }}</p>
  <p>{{ arr2 }}</p>
  <p>{{ modifyArray(arr2) }}</p>
  <p>{{ arr3 }}</p>
  <p>{{ modifyArray(arr3) }}</p>
</template>

<script setup lang="ts">
  const arr1 = ["Avocado", "Tomato", "Potato","Mango", "Lemon","Carrot"]
  const arr2 = ["Google", "Facebook","Apple", "Amazon","Microsoft",  "IBM"]
  const arr3 = ["Google", "Facebook","Apple", "Amazon"]

  function modifyArray(arr: string[]) {
    if (arr.length < 5) return 'item not found'
    return arr.map((e, index) => {
      if (index === 4) return e.toUpperCase()
      return e
    })
  }
</script>