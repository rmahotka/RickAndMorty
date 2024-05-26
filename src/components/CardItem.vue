<template>
  <div class="block">
    <div class="block-img" :style="getImg"></div>
    <div class="block-info">
      <div>
        <p class="title-item">{{ character.name }}</p>
        <div class="status-block">
          <p class="status-item" :style="statusCharacter(character.status)"></p>
          <span>{{ character.status }} - {{ character.species }}</span>
        </div>
      </div>
      <div class="block-item">
        <p class="block-item-title">Last know location:</p>
        <p class="block-item-text">{{ character.location.name }}</p>
      </div>
      <div class="block-item">
        <p class="block-item-title">First seen in:</p>
        <p class="block-item-text">{{ nameEpisode }}</p>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'

const props = defineProps({
  character: {
    type: Object,
    required: true
  }
})

const urlEdpisode = ref(props.character.episode[0])
const nameEpisode = ref('')

const getImg = computed(() => {
  return { 'background-image': `url(${props.character.image})` }
})

const statusCharacter = (status) => {
  if (status === 'Alive') {
    return 'background-color:green'
  } else if (status === 'Dead') {
    return 'background-color:red'
  } else {
    return 'background-color:yellow'
  }
}

const FirstEpisode = () => {
  fetch(urlEdpisode.value)
    .then((responce) => responce.json())
    .then((result) => (nameEpisode.value = result.name))
    .catch((err) => console.error(err))
}

onMounted(FirstEpisode)
</script>

<style lang="scss" scoped>
.block {
  border-radius: 10px;
  background-color: #3c3e44;
  color: #fff;
  display: flex;
  align-items: center;

  &-img {
    height: 240px;
    width: 240px;
    position: relative;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-size: cover;
    background-repeat: no-repeat;
    background-position: center center;
    border-radius: 10px 0 0 10px;
  }
}

.block-info {
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  height: 200px;
  padding: 20px;
}

.title-item {
  font-size: 30px;
  font-weight: 700;
}

.block-item {
  &-title {
    color: #9e9c9b;
    font-size: 18px;
  }

  &-text {
    font-size: 21px;
  }
}

.status-block {
  display: flex;
  align-items: center;
  gap: 8px;

  span {
    font-weight: 600;
  }
}

.status-item {
  width: 10px;
  height: 10px;
  border-radius: 50%;
}
</style>
