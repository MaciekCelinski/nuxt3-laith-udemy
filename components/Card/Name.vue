<template>
  <div class="card">
    <h4>{{name}}</h4>
    <p @click="removeName">x</p>
  </div>
</template>

<script setup context lang="ts">
import { defineProps, defineEmits } from 'vue';

interface NameProps {
  name: string
}

const props = defineProps<NameProps>()

const emit = defineEmits(['remove'])

const removeName = () => {
  emit('remove', props.name)
}

</script>


<style scoped>
.card {
  background: rgb(27, 60, 138);
  color: white;
  border-radius: 1rem;
  margin-right: 0.5rem;
  margin-bottom: 1rem;
  display: flex;
  justify-content: center;
  width: 20%;
}

.card p {
  position: absolute;
  cursor: pointer;
  margin-left: 7%;
  margin-top: 5px;
}
</style>