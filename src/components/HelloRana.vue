<template>
    <div class="container">
      <!-- Form for adding new item -->
      <form @submit.prevent="addItem" class="mt-3 border p-3 bg-light">
        <input type="text" v-model="newItemName" class="form-control mb-2" placeholder="Enter item name">
        <button type="submit" class="btn btn-primary">Add Item</button>
      </form>
  
      <!-- List of items -->
      <ul class="list-group mt-3">
        <li v-for="(item, index) in items" :key="item.id" class="list-group-item border p-3">
          {{ item.name }}
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
        items: [
          { id: 1, name: 'Item 1' },
          { id: 2, name: 'Item 2' },
          { id: 3, name: 'Item 3' }
        ],
        newItemName: '',
        editedItemName: '',
        isEditing: null
      };
    },
    methods: {
      addItem() {
        if (this.newItemName.trim() !== '') {
          this.items.push({
            id: this.items.length + 1,
            name: this.newItemName
          });
          this.newItemName = '';
        }
      },
      editItem(index) {
        this.editedItemName = this.items[index].name;
        this.isEditing = index;
      },
      updateItem() {
        if (this.editedItemName.trim() !== '') {
          this.items[this.isEditing].name = this.editedItemName;
          this.cancelEdit();
        }
      },
      cancelEdit() {
        this.isEditing = null;
        this.editedItemName = '';
      },
      deleteItem(index) {
        this.items.splice(index, 1);
      }
    }
  };
  </script>
  
  <style scoped>
  /* Add custom CSS styles here if needed */
  </style>
  