<template>
  <div class="form-container">
    <h2>Add Item</h2>
    <form @submit.prevent="handleSubmit">

      <div class="form-group">
        <label for="food_name">Food Name</label>
        <input id="food_name" v-model="newItem.food_name" placeholder="e.g., tomatoes" required />
      </div>

      <div class="form-group">
        <label for="quantity">Quantity</label>
        <input id="quantity" v-model.number="newItem.quantity" type="number" placeholder="Quantity" required />
      </div>

      <div class="form-group">
        <label for="date_purchased">Date Purchased</label>
        <input id="date_purchased" v-model="newItem.date_purchase" type="date" required />
      </div>

      <div class="form-actions">
        <button type="submit" class="btn btn-primary">Add Item</button>
        <button type="button" class="btn btn-secondary" @click="$emit('close')">Cancel</button>
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref, watch, defineEmits } from 'vue';

const emit = defineEmits(['item-added', 'close']);
const newItem = ref({ food_name: '', quantity: 0, date_purchase: '' });

watch(newItem, (newVal) => {
  console.log('New item:', newVal); // Debugging log
});

const handleSubmit = function() {
  console.log('handleSubmit called'); // Debugging log
  console.log('Emitting item-added event with:', newItem.value); // Debugging log
  emit('item-added', newItem.value);
  newItem.value = { food_name: '', quantity: 0, date_purchase: '' };
  emit('close');
};
</script>


<style scoped>
.form-container {
  background-color: var(--darkerMountainShadow);
  padding: 20px;
  border-radius: 10px;
  box-shadow: 0 0 15px rgba(0, 0, 0, 0.1);
  max-width: 400px;
  margin: 0 auto;
}

h2 {
  text-align: center;
  margin-bottom: 20px;
  color: var(--freshVeg);
}

.form-group {
  margin-bottom: 15px;
}

label {
  display: block;
  margin-bottom: 10px;
  font-weight: bold;
  color: var(--glacierWater);
  font-size: large;
}

input, select {
  width: 100%;
  padding: 20px;
  border: 3px solid var(--lighterMountainShadow);
  border-radius: 5px;
  box-sizing: border-box;
  font-size: 16px;
  background-color: var(--cloudyTransparent);
  color: var(--darkerMountainShadow);
}

input:focus, select:focus {
  border-color: var(--freshVeg);
  color: black;
  outline: none;
}

.form-actions {
  display: flex;
  justify-content: space-between;
}

.btn {
  padding: 10px 20px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 16px;
}

.btn-primary {
  background-color: #4caf50;
  color: white;
}

.btn-primary:hover {
  background-color: #45a049;
}

.btn-secondary {
  background-color: #f44336;
  color: white;
}

.btn-secondary:hover {
  background-color: #e53935;
}
</style>
