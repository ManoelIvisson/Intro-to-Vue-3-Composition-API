<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([
  {id: 1, label: '10 party hats'},
  {id: 2, label: '2 board games'},
  {id: 3, label: '20 cups'}
])
const newItem = ref('')
const newItemHighPriority = ref(false)
</script>

<template>
  
  <input type="text" v-model="newItem" placeholder="Add a New Item">
  Priority:
  <label>
    <input type="checkbox" v-model="newItemHighPriority" value=true>
    High Priority
  </label>

  <h1>{{ header }}</h1>
  <ul>
    <li v-for="{id, label} in items" :key="id">{{ label }}</li>
  </ul>
  
</template>

