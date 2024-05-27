<template>
  <HeaderItem />
  <div class="container">
    <form class="filter" @submit.prevent="filter(filterName, filterStatus)">
      <input type="text" v-model="filterName" />
      <select name="status" id="filter-status" v-model="filterStatus">
        <option value=""></option>
        <option value="alive">Alive</option>
        <option value="dead">Dead</option>
        <option value="unknown">Unknown</option>
      </select>
      <button>Применить</button>
    </form>
    <CardComponent :characters="characters" />
    <div class="pagination-block">
      <button @click="prevPage" class="pagination-btn" :disabled="isFirstPage"><</button>
      <span class="pageNumber">{{ pageItem }}</span>
      <button @click="nextPage" class="pagination-btn" :disabled="isLasttPage">></button>
    </div>
  </div>
</template>

<script setup>
import HeaderItem from './components/HeaderItem.vue'
import CardComponent from './components/CardComponent.vue'
import { computed, onMounted, ref } from 'vue'

const filterStatus = ref('')
const filterName = ref('')
const characters = ref()
const pageItem = ref(1)

const filter = (name, status, page) => {
  fetch(`https://rickandmortyapi.com/api/character?name=${name}&status=${status}&page=${page}`)
    .then((responce) => responce.json())
    .then((result) => {
      characters.value = result.results
    })
}

const nextPage = () => {
  pageItem.value++
  window.scrollTo(pageYOffset, 0)
  filter(filterName.value, filterStatus.value, pageItem.value)
}

const prevPage = () => {
  pageItem.value--
  window.scrollTo(pageYOffset, 0)
  filter(filterName.value, filterStatus.value, pageItem.value)
}

const isFirstPage = computed(() => {
  return pageItem.value === 1
})

const isLasttPage = computed(() => {
  return pageItem.value === 41
})

onMounted(() => {
  filter(filterName.value, filterStatus.value)
})
</script>

<style lang="scss" scoped>
.container {
  padding: 0 30px;
  background-color: #272b33;
}

.filter {
  display: flex;
  gap: 8px;
  padding: 20px 0;

  input {
    padding: 6px 8px;
    border-radius: 6px;
    border: 0;
  }

  button {
    padding: 6px;
    border-radius: 6px;
    border: 1px solid #fff;
    color: #fff;
    background: inherit;
    cursor: pointer;
    font-size: 16px;
    transition: all ease 0.3s;

    &:hover {
      background-color: #fff;
      color: #0d0f11;
    }
  }
}

.pageNumber {
  font-size: 25px;
  color: #fff;
}

.pagination-block {
  display: flex;
  justify-content: center;
  align-items: center;
  padding-bottom: 20px;
  gap: 20px;
}

.pagination-btn {
  padding: 15px;
  border-radius: 10px;
  border: 1px solid #fff;
  color: #fff;
  font-size: 20px;
  background: inherit;
  cursor: pointer;
  transition: all ease 0.3s;

  &:hover {
    background: #fff;
    color: #0d0f11;
  }
}
</style>
