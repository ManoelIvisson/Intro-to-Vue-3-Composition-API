<script setup>
import { ref } from 'vue'

const header = ref('Shopping List App')
const items = ref([])
const newItem = ref('')
const newItemHighPriority = ref(false)
const editing = ref(false)

function saveItem() {
  items.value.push({id: items.value.length + 1, label: newItem.value})
  newItem.value = ""
}

function doEdit(e) {
  editing.value = e
  newItem.value = ""
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
    <button class="btn btn-primary">Save Item</button>
  </form>

  <ul>
    <li v-for="{id, label} in items" :key="id">{{ label }}</li>
  </ul>

  <p v-if="!items.length">
    Nothing to see here
  </p>
  
</template>

