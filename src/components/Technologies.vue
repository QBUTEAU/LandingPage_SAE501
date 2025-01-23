<template>
  <div class="techno">
    <h2>OUTILS ET TECHNOLOGIES</h2>
    <ul class="techno__list">
      <li v-for="tech in technologies" :key="tech.name" :class="['techno__item', tech.class]">
        <div class="techno__img">
          <img :src="getImageUrl(tech.img)" :alt="tech.name">
        </div>
        <p>{{ tech.name }}</p>
      </li>
    </ul>
  </div>
</template>

<script>
import technologiesData from '../assets/json/techno.json';

export default {
  name: 'Technologies',
  data() {
    return {
      technologies: technologiesData
    };
  },
  methods: {
    getImageUrl(imagePath) {
      return new URL(`../assets/img/${imagePath}`, import.meta.url).href;
    }
  }
}
</script>

<style scoped>
.techno__img img {
  height: 90%;
}
.godot .techno__img img {
  height: 110%;
}
</style>