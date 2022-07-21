<template>
  <div class="container" >
    <h1>Baby Name Generator</h1>
    <p>Choose your options and click the "Find Names" button below</p>
    <div class="options-container">
      <Option v-for="option in optionsArray" :key="option.title" :option=option :options=options />
      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>
    <div class="cards-container">
      <CardName @remove="removeNameFromList" v-for="name, index in selectedNames" :key="index" :name="name"/>
    </div>
  </div>
</template>

<script setup lang="ts">
import { reactive, ref } from 'vue';
import { 
  Gender, 
  Popularity, 
  Length, names 
} from './data'

interface OptionsTypes {
  gender: Gender,
  popularity: Popularity,
  length: Length
}

const options = reactive<OptionsTypes>({
  gender: Gender.GIRL,
  popularity: Popularity.UNIQUE,
  length: Length.SHORT
})

const selectedNames = ref<string[]>([]);

const computeSelectedNames = () => {
  const filtredNames = names.filter(name => name.gender === options.gender).filter(name => name.popularity === options.popularity).filter(name => {
    if (options.length === Length.ALL) return true
    else return name.length === options.length
  })

  selectedNames.value = filtredNames.map(name => name.name)
}


const removeNameFromList = (name:string) => {
  selectedNames.value = selectedNames.value.filter(el => el !== name)
}

const optionsArray = [
  {
    title: "1) Choose a gender",
    category: 'gender',
    buttons: [Gender.BOY, Gender.GIRL, Gender.UNISEX]
  },
  {
    title: "2) Choose names popularity",
    category: 'popularity',
    buttons: [Popularity.TRENDY, Popularity.UNIQUE]
  },
  {
    title: "3) Choose names length",
    category: 'length',
    buttons: [Length.SHORT, Length.ALL, Length.LONG]
  },
]

</script>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

h1 {
  font-size: 3rem;
}

.options-container {
  background: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 95%;
  margin: 0 auto;
  margin-top: 4rem;
  position: relative;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 3rem;
}

.primary {
  background: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  border: none;
  padding: 0.75rem 4rem;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}
</style>
