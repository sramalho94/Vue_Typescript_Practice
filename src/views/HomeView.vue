<script setup lang="ts">
import { ref } from 'vue'

// restaurants
// Name - string
// Address - string
// Status - string "Want to try" | "Must try"
// Dishes - array of Dish objects

interface Restaurant {
  name?: string
  address?: string
  status?: string
  dishes?: Dish[]
}

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})
const addRestaurant = () => {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    address: '',
    status: '',
    dishes: []
  })
}
</script>

<template>
  <main>
    <pre>{{ newRestaurant }}</pre>
    <!-- create a form that allows users to add a restaurant to list -->
    <form @submit.prevent="addRestaurant">
      <label for="restaurant-name">Restaurant Name</label>
      <input id="restaurant-name" v-model="newRestaurant.name" type="text" />
      <label for="restaurant-address">Restaurant Address</label>
      <input id="restaurant-name" v-model="newRestaurant.address" />
      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">
        {{ restaurant }}
      </li>
    </ul>
  </main>
</template>
