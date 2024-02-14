<template>
  <div>
    <h1>Data Fetching Example</h1>
    <ul>
      <li v-for="(pokemon, index) in pokemons" :key="index">
        <a :href="pokemon.url">{{ pokemon.name }}</a>
      </li>
    </ul>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from 'axios'

const pokemons = ref([
  {
    name: String,
    url: String
  }
])

const fetchData = async () => {
  try {
    const response = await axios.get('https://pokeapi.co/api/v2/pokemon?limit=100000&offset=0')
    pokemons.value = response.data.results
  } catch (error) {
    console.error('Error fetching data:', error)
  }
}

onMounted(async () => {
  await fetchData()
})
</script>
