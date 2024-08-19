<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([])
const newItem = ref('')
const newItemHighPriority = ref(false)
const editing = ref(false)

function saveItem() {
  items.value.push({
    id: items.value.length + 1, 
    label: newItem.value,
    highPriority: newItemHighPriority.value
  })
  newItem.value = ""
}

function doEdit(e) {
  editing.value = e
  newItem.value = ""
}

function togglePurchased(item) {
  item.purchased = !item.purchased
}

</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
    <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">Add Item</button>
  </div>

  <form v-if="editing" class="add-item-form" @submit.prevent="saveItem">
    <input type="text" v-model="newItem" placeholder="Add a New Item">
    <label>
      <input type="checkbox" v-model="newItemHighPriority" value=true>
      High Priority
    </label>
    <button :disabled="newItem.length === 0" class="btn btn-primary">Save Item</button>
  </form>

  <ul>
    <li v-for="item in items" :key="item.id" @click="togglePurchased(item)" class="static-class"
    :class="{ strikeout: item.purchased, priority: item.highPriority }">
      {{ item.label }}
    </li>
  </ul>

  <p v-if="!items.length">
    Nothing to see here
  </p>
  
</template>

