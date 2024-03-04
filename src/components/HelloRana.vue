<template>
    <div class="container">
      <!-- Form for adding new item -->
      <form @submit.prevent="addItem" class="mt-3 border p-3 bg-light">
        <input type="text" v-model="newItemName" class="form-control mb-2" placeholder="Enter item name">
        <button type="submit" class="btn btn-primary">Add Item</button>
      </form>
  
      <!-- List of items -->
      <ul class="list-group mt-3">
        <li v-for="(item, index) in items" :key="item" class="list-group-item border p-3">
          {{ item }}
          <button @click="editItem(index)" class="btn btn-sm btn-info ms-2">Edit</button>
          <button @click="deleteItem(index)" class="btn btn-sm btn-danger ms-2">Delete</button>
        </li>
      </ul>
  
      <!-- Form for editing item -->
      <div v-if="isEditing !== null" class="mt-3 border p-3 bg-light">
        <input type="text" v-model="editedItemName" class="form-control mb-2" placeholder="Edit item name">
        <button @click="updateItem" class="btn btn-primary mr-2">Update</button>
        <button @click="cancelEdit" class="btn btn-secondary">Cancel</button>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'HelloRana',
    data() {
      return {
        items: ['item-1','item-2','item-3'],
        newItemName: '',
        editedItemName: '',
        isEditing: null
      };
    },
    methods: {
      addItem() {
        if (this.newItemName.trim() !== '') {
          this.items.push(this.newItemName);
          this.newItemName = '';
        }
      },
      deleteItem(index) {
          this.items.splice(index, 1);
      },
      editItem(index) {
          this.editedItemName = this.items[index];
          this.isEditing = index;
      },
      updateItem() {
        this.items[this.isEditing] = this.editedItemName;
        this.isEditing = null;
        this.editedItemName = '';
      },
      cancelEdit() {
        this.isEditing = null;
        this.editedItemName = '';
      }

     
    }
  };
  </script>
  
  <style scoped>
  /* Add custom CSS styles here if needed */
  </style>
  ``