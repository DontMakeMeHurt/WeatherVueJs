<template>
  <main>
    <!-- Date -->
    <div class="text-center text-purple-700 mb-6">
      {{
        new Date().toLocaleString('en-us', {
          weekday: 'long',
          year: 'numeric',
          month: 'long',
          day: 'numeric'
        })
      }}
    </div>
    <!-- Search -->
    <div>
      <SearchInput @place-data="addData" />
    </div>

    <!-- weather Card -->
    <div v-for="(place, index) in places" :key="index">
      <WeatherCard :place="place" @delete-place="deletePlace" />
    </div>
  </main>
</template>

<script setup>
import { ref } from 'vue'
import SearchInput from './components/SearchInput.vue'
import WeatherCard from './components/WeatherCard.vue'

const addData = (data) => {
  places.value.push(data)
}

const deletePlace = (name) => {
  if (confirm('Are you sure ?')) {
    places.value = places.value.filter((p) => p.location.name !== name)
  }
}

const places = ref([])
</script>
