<template>
  <div class="h-screen relative overflow-hidden">
    <img />
    <div class="absolute w-full h-full top-0 overlay" />
    <div class="absolute w-full h-full top-0 p-48">
      <div class="flex justify-between">
        <div>
          <h1 class="text-7xl text-white">{{ city.name }}</h1>
          <p class="font-extralight text-2xl mt-2 text-white">{{ currentDate() }}</p>
          <img :src="`https://openweathermap.org/img/wn/${city.weather[0].icon}@4x.png`" class="w-56 icon" />
        </div>
        <div>
          <!-- <p class="text-9xl text-white font-extralight">{{city.main.temp}}</p> -->
          <p class="text-9xl text-white font-extralight">{{ celciusTemp() }}</p>
        </div>
      </div>
      <div class="mt-20">
        <input type="text" class="w-1/2" placeholder="Search a city..." v-model='cityInput'/>
        <button class="bg-sky-400 w-20 text-white h-10" @click="setLocation">
          Search
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import {ref} from 'vue'

const location = ref('Toronto')
const cityInput = ref('')

// const {data: city, error} = useFetch('https://api.openweathermap.org/data/2.5/weather?q=Warsaw&appid=9fafc3710a5d524a7d325add0311688f&units=metric')
const { data: city, error } = useFetch( () => `https://api.openweathermap.org/data/2.5/weather?q=${location.value}&appid=9fafc3710a5d524a7d325add0311688f`)

const celciusTemp = () => `${Math.floor(city.value['main'].temp) - 273}°C`
const currentDate = () => {

  interface optionsType { }

  const options: optionsType = { weekday: 'long', month: 'long', day: 'numeric' }
  return new Date().toLocaleDateString('en-US', options)
}

const setLocation = () => {
  location.value = cityInput.value
}

</script>

<style scoped>
.overlay {
  background: rgba(0, 0, 0, 0.5);
}

.icon {
  margin: -2.75rem auto auto -2.75rem;
}
</style>