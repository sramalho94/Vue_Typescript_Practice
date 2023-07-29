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
  status?: RecommendStatus
  dishes?: Dish[]
}

interface Dish {
  name: string
  diet?: Diet
  status?: RecommendStatus
}

type Diet =
  | 'vegetarian'
  | 'vegan'
  | 'gluten-free'
  | 'pescatarian'
  | 'lactose-free'
  | 'other'

// type RecommendStatus =
//   | 'Want to Try'
//   | 'Recommended'
//   | 'Do Not Recommend'
//   | 'Must Try'

const restaurantList = ref<Restaurant[]>([])
const newRestaurant = ref<Restaurant>({})

// Extract value from
const restaurantStatusList = [
  'Want to Try',
  'Recommended',
  'Do Not Recommend',
  'Must Try'
] as const

type RecommendStatus = (typeof restaurantStatusList)[number]

const addRestaurant = () => {
  restaurantList.value.push({
    name: newRestaurant.value.name,
    address: newRestaurant.value.address,
    status: newRestaurant.value.status,
    dishes: []
  })
}
</script>

<template>
  <main>
    <pre>{{ newRestaurant }}</pre>
    <!-- create a form that allows users to add a restaurant to list -->
    <form @submit.prevent="addRestaurant">
      <div>
        <label for="restaurant-name">Restaurant Name</label>
        <input id="restaurant-name" v-model="newRestaurant.name" type="text" />
      </div>
      <div>
        <label for="restaurant-address">Restaurant Address</label>
        <input id="restaurant-address" v-model="newRestaurant.address" />
      </div>
      <div>
        <label for="restaurant-status">Restaurant Status</label>
        <select
          name="restaurant-status"
          id="restaurant-status"
          v-model="newRestaurant.status"
        >
          <option
            v-for="status in restaurantStatusList"
            :value="status"
            :key="status"
          >
            {{ status }}
          </option>
        </select>
      </div>
      <button type="submit">Add Restaurant</button>
    </form>
    <ul>
      <li v-for="restaurant in restaurantList" :key="restaurant.name">
        {{ restaurant.name }} - {{ restaurant.status }}
      </li>
    </ul>
  </main>
</template>
