<template>
  <h1>17. The following shopping cart has four products. Create an addProduct, removeProduct ,editProduct , removeAll functions to modify the shopping cart.</h1>
  <div class="example"><pre>
const shoppingCart = ['Milk','Coffee','Tea', 'Honey'];

addProduct( "Meat");
["Milk", "Coffee", "Tea", "Honey", "Meat"]

editProduct(3, "Sugar" );
["Milk", "Coffee", "Tea", "Sugar", "Meat"]

removeProduct(0);
["Coffee", "Tea", "Sugar", "Meat"]
removeProduct(3);
["Coffee", "Tea", "Sugar"]
  </pre></div>
  <form @submit.prevent>
    <fieldset>
      <legend>Product name and position</legend>
      <input v-model="product" required/>
      <select v-model="position">
        <option v-for="o in shoppingCart.length" :key="o">{{ o }}</option>
      </select>
    </fieldset>
    <button @click="addProduct(product)">Add</button>
    
    <button @click="editProduct(position,product)">Edit</button>
    <button @click="removeProduct(position)">Remove</button>
    <button @click="removeAll()">RemoveAll</button>
  </form>
  <ul>
    <li v-for="(item, index) in shoppingCart" :key="item">{{ index + 1 }} - {{ item }}</li>
  </ul>
</template>
<script setup lang="ts">
import { ref } from 'vue'
const product = ref<string>('')
const position = ref<number>(1)
const shoppingCart = ref<string[]>(['Milk','Coffee','Tea', 'Honey'])

function addProduct(product: string) { if (product) shoppingCart.value.push(product) }
function editProduct(position: number, newProduct: string) { if (newProduct && position) shoppingCart.value[position - 1] = newProduct }
function removeProduct(position: number) { if (position) shoppingCart.value.splice(position - 1, 1) }
function removeAll() { shoppingCart.value = [] }
</script>