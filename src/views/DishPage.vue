<script setup lang="ts">
import { ref } from 'vue'

interface Dish {
  name?: string
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

const dishList = ref<Dish[]>([])
const newDish = ref<Dish>({})

// Extract value from
const dishStatusList = [
  'Want to Try',
  'Recommended',
  'Do Not Recommend',
  'Must Try'
] as const

const dietList = [
  'vegetarian',
  'vegan',
  'gluten-free',
  'pescatarian',
  'lactose-free',
  'other'
] as const
type RecommendStatus = (typeof dishStatusList)[number]
type DietStatus = (typeof dietList)[number]

const addDish = () => {
  dishList.value.push({
    name: newDish.value.name,
    diet: newDish.value.diet,
    status: newDish.value.status
  })
}
</script>

<template>
  <main>
    <pre>{{ newDish }}</pre>
    <!-- create a form that allows users to add a restaurant to list -->
    <form @submit.prevent="addDish">
      <div>
        <label for="dish-name">Dish Name</label>
        <input id="dish-name" v-model="newDish.name" type="text" />
      </div>
      <div>
        <label for="dish-diet">Dish Diet</label>
        <select name="dish-cuisine" v-model="newDish.diet">
          <option v-for="diet in dietList" :key="diet">
            {{ diet }}
          </option>
        </select>
      </div>
      <div>
        <label for="dish-status">Dish Status</label>
        <select name="dish-status" id="dish-status" v-model="newDish.status">
          <option
            v-for="status in dishStatusList"
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
      <li v-for="dish in dishList" :key="dish.name">
        {{ dish.name }} - {{ dish.status }}
      </li>
    </ul>
  </main>
</template>
