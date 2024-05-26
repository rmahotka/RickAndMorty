<template>
  <section class="block-container">
    <form class="filter" @submit.prevent="filter">
      <input type="text" v-model="filterName" />
      <select name="status" id="filter-status">
        <option value=""></option>
        <option value="alive">Alive</option>
        <option value="dead">Dead</option>
        <option value="unknown">Unknown</option>
      </select>
      <button>Применить</button>
    </form>
    <div class="item-container">
      <div v-for="item in props.characters" :key="item.id" class="block-item">
        <CardItem :character="item" />
      </div>
    </div>
  </section>
</template>

<script setup>
import CardItem from './CardItem.vue'

const props = defineProps({
  characters: {
    type: Object,
    required: true
  }
})

const filter = () => {}
</script>

<style lang="scss" scoped>
.block-container {
  padding: 80px 0;
}

.item-container {
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 30px;
}

.block-item {
  grid-column: 6 span;
}

.filter {
  display: flex;
  gap: 8px;
  margin-bottom: 20px;

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
</style>
