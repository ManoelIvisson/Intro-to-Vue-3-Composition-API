<script setup>
import { ref, computed } from 'vue'

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
  newItemHighPriority.value = ""
}

function doEdit(e) {
  editing.value = e
  newItem.value = ""
}

function togglePurchased(item) {
  item.purchased = !item.purchased
}

const characterCount = computed(() => newItem.value.length)

const reversedItems = computed(() => [...items.value].reverse())

</script>

<template>
  <div class="header">
    <h1>{{ header }}</h1>
    <button v-if="editing" class="btn" @click="doEdit(false)">Cancel</button>
    <button v-else class="btn btn-primary" @click="doEdit(true)">Add Item</button>
  </div>

  <form v-if="editing" class="add-item-form" @submit.prevent="saveItem">
    <input type="text" v-model="newItem" placeholder="Add a New Item" maxlength="100">
    <label>
      <input type="checkbox" v-model="newItemHighPriority" value=true>
      High Priority
    </label>
    <button :disabled="newItem.length === 0" class="btn btn-primary">Save Item</button>
  </form>

  <p v-if="editing" class="counter">
    {{ characterCount }}/100
  </p>

  <ul>
    <li v-for="item in reversedItems" :key="item.id" @click="togglePurchased(item)" class="static-class"
    :class="{ strikeout: item.purchased, priority: item.highPriority }">
      {{ item.label }}
    </li>
  </ul>

  <p v-if="!items.length">
    Nothing to see here
  </p>
  
</template>

