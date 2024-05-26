<template>
  <HeaderItem />
  <div class="container">
    <CardComponent :characters="charactersResult" />
  </div>
</template>

<script setup>
import HeaderItem from './components/HeaderItem.vue'
import CardComponent from './components/CardComponent.vue'
import { onMounted, ref } from 'vue'

const charactersResult = ref([])
const charactersInfo = ref({})

const getData = () => {
  fetch('https://rickandmortyapi.com/api/character')
    .then((responce) => responce.json())
    .then((res) => {
      charactersResult.value = res.results
      charactersInfo.value = res.info
    })
    .catch((err) => {
      console.error(err)
    })
}

onMounted(getData)
</script>

<style lang="scss" scoped>
.container {
  padding: 0 30px;
  background-color: #272b33;
}
</style>
