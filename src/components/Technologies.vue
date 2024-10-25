<template>
    <div class="techno">
        <h2>OUTILS ET TECHNOLOGIES</h2>
        <ul class="techno__list">
            <li v-for="tech in technologies" :key="tech.name" class="techno__item">
                <img class="techno__img" :src="getImageUrl(tech.img)" :alt="tech.name">
                <p class="techno__nom">{{ tech.name }}</p>
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