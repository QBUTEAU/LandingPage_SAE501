<template>
  <div class="infos__news" ref="infosNews">
    <h2>ACTUALITÉS</h2>
    <div v-if="newsList.length">
      <div v-for="(newsItem, index) in paginatedNews" :key="index"
        :class="['news', { 'most-recent': isMostRecent(newsItem) }]">
        <div class="news__img" :style="{ backgroundImage: `url(${getImageUrl(newsItem.linkImg)})` }"></div>
        <p class="news__text">
          <span>{{ newsItem.author }} - {{ newsItem.date }}</span><br>
          {{ newsItem.text }}
        </p>
      </div>
      <div class="pagination">
        <button @click="prevPage" :disabled="currentPage === 1"
          :class="{ disabled: currentPage === 1 }">Précédente</button>
        <span>Page {{ currentPage }} sur {{ totalPages }}</span>
        <button @click="nextPage" :disabled="currentPage === totalPages"
          :class="{ disabled: currentPage === totalPages }">Suivante</button>
      </div>
    </div>
    <div v-else>
      <p>Chargement des news...</p>
    </div>
  </div>
</template>

<script>
import newsData from '../assets/json/news.json';

export default {
  name: 'News',
  data() {
    return {
      newsList: newsData,
      currentPage: 1,
      itemsPerPage: 4
    };
  },
  computed: {
    totalPages() {
      return Math.ceil(this.newsList.length / this.itemsPerPage);
    },
    paginatedNews() {
      const start = (this.currentPage - 1) * this.itemsPerPage;
      const end = start + this.itemsPerPage;
      return this.newsList.slice(start, end);
    },
    mostRecentNews() {
      return this.newsList.reduce((latest, newsItem) => {
        return new Date(newsItem.date) > new Date(latest.date) ? newsItem : latest;
      }, this.newsList[0]);
    }
  },
  methods: {
    getImageUrl(imageName) {
      return new URL(`../assets/img/${imageName}`, import.meta.url).href;
    },
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.currentPage++;
        this.scrollToTop();
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.currentPage--;
        this.scrollToTop();
      }
    },
    scrollToTop() {
      this.$nextTick(() => {
        const targetElement = this.$refs.infosNews;
        if (targetElement) {
          const offsetTop = targetElement.getBoundingClientRect().top + window.pageYOffset - 30;
          window.scrollTo({
            top: offsetTop,
            behavior: 'smooth'
          });
        }
      });
    },
    isMostRecent(newsItem) {
      return newsItem === this.mostRecentNews;
    }
  }
}
</script>

<style scoped>
.pagination button.disabled {
  background-color: rgb(195, 195, 195);
  cursor: not-allowed;
}
</style>