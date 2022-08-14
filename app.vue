<template>
  <div class="h-screen relative overflow-hidden">
    <img />
    <div class="absolute w-full h-full top-0 overlay" />
    <div class="absolute w-full h-full top-0 p-48">
      <div class="flex justify-between">
        <div>
          <h1 class="text-7xl text-white">Toronto</h1>
          <p class="font-extralight text-2xl mt-2 text-white">Sunday December 9th</p>
          <img class="w-56 icon" />
        </div>
        <div>
          <p class="text-9xl text-white font-extralight">23°C</p>
        </div>
      </div>
      <div class="mt-20">
        <input type="text" class="w-1/2" placeholder="Search a city..."/>
        <button class="bg-sky-400 w-20 text-white h-10">
          Search
        </button>
      </div>
    </div>
  </div>
</template>

<style scoped>
.overlay {
  background: rgba(0, 0, 0, 0.5);
}
</style>