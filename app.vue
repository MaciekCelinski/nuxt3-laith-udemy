<template>
  <div class="h-screen relative overflow-hidden">
    <img :src="bgImg" />
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
        <input type="text" class="w-1/2" placeholder="Search a city..." v-model='cityInput' />
        <button class="bg-sky-400 w-20 text-white h-10" @click="setLocation">
          Search
        </button>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'

const location = ref('Oslo')
const cityInput = ref('')
const bgImg = ref('')

// const {data: city, error} = useFetch('https://api.openweathermap.org/data/2.5/weather?q=Warsaw&appid=9fafc3710a5d524a7d325add0311688f&units=metric')
// const { data: city, error } = useFetch( () => `https://api.openweathermap.org/data/2.5/weather?q=${location.value}&appid=9fafc3710a5d524a7d325add0311688f`)
const { data: city, refresh, error } = useAsyncData('city', async () => {

  const response = await $fetch(`https://api.openweathermap.org/data/2.5/weather?q=${location.value}&units=metric&appid=9fafc3710a5d524a7d325add0311688f`)

  const temp = response['main'].temp;

  if (temp <= -10) {
    bgImg.value =
      "https://images.unsplash.com/photo-1483664852095-d6cc6870702d?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=3540&q=80";
  } else if (temp > -10 && temp <= 0) {
    bgImg.value =
      "https://images.unsplash.com/photo-1476820865390-c52aeebb9891?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=3540&q=80";
  } else if (temp > 0 && temp <= 25) {
    bgImg.value =
      "https://images.unsplash.com/photo-1560258018-c7db7645254e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=4032&q=80";
  } else {
    bgImg.value =
      "https://images.unsplash.com/photo-1507525428034-b723cf961d3e?ixlib=rb-1.2.1&ixid=MnwxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8&auto=format&fit=crop&w=3546&q=80";
  }

  return response
}, {
  watch: [location]
})

const celciusTemp = () => `${Math.floor(city.value['main'].temp)}°C`
const currentDate = () => new Date().toLocaleDateString('en-US', { weekday: 'long', month: 'long', day: 'numeric' })
const setLocation = () => {
  location.value = cityInput.value
  // refresh()
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