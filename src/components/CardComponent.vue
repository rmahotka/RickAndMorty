<template>
  <section class="block-container">
    <div v-for="item in props.characters" :key="item.id" class="block-item">
      <CardItem :character="item" />
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
</script>

<style lang="scss" scoped>
.block-container {
  padding: 80px 0;
  display: grid;
  grid-template-columns: repeat(12, 1fr);
  gap: 30px;
}

.block-item {
  grid-column: 6 span;
}
</style>
