<script>
import Member from './components/Member.vue';
import membersData from './assets/json/members.json';
import News from './components/News.vue';
import Description from './components/Description.vue';
import NoteCadrage from './components/NoteCadrage.vue';
import Planning from './components/Planning.vue';
import EtatArtDomaine from './components/EtatArtDomaine.vue';
import Avancee from './components/Avancee.vue';
import Technologies from './components/Technologies.vue';

export default {
  components: {
    Member,
    News,
    NoteCadrage,
    Planning,
    Description,
    EtatArtDomaine,
    Avancee,
    Technologies
  },
  data() {
    return {
      membersList: membersData,
      currentComponent: 'Description', // Default component to display
      windowWidth: window.innerWidth,  // Track the window width
      showSAEProgress: true
    };
  },
  computed: {
    shouldShowAllComponents() {
      // Return true if the window width is less than 950px
      return this.windowWidth < 950;
    }
  },
  methods: {
    setComponent(componentName) {
      if (!this.shouldShowAllComponents) {
        this.currentComponent = componentName;

        // Scroll to .infos__projet div after changing the component
        this.$nextTick(() => {
          const targetElement = this.$refs.infosProjet;
          if (targetElement) {
            const offsetTop = targetElement.getBoundingClientRect().top + window.pageYOffset - 30;
            window.scrollTo({
              top: offsetTop,
              behavior: 'smooth'
            });
          }
        });
      }
    },
    toggleProgress() {
      this.showSAEProgress = !this.showSAEProgress;
    },
    handleResize() {
      this.windowWidth = window.innerWidth;
    }
  },
  mounted() {
    window.addEventListener('resize', this.handleResize);
  },
  beforeDestroy() {
    window.removeEventListener('resize', this.handleResize);
  }
}
</script>

<template>
  <header class="hero-header">
    <h1>SpeedDocker</h1>
    <h4>Le premier speedrun de l'univers MMI !</h4>
  </header>

  <div class="presentation">
    <div class="presentation__screen">
      <div class="presentation-screen__img"></div>
      <ul class="presentation-screen__type">
        <li class="type"><i class="fa-regular fa-compass"></i>Jeu de plateforme</li>
        <li class="type"><i class="fa-solid fa-location-dot"></i>Troyes, France</li>
      </ul>
    </div>
    <div class="presentation__infos">
      <div class="presentation-infos__bar">
        <div v-if="showSAEProgress">
          <p class="span-sae"><span>72%</span> du temps de travail passé.</p>
          <div class="progress-bar__sae">
            <div class="progress-bar-sae__lvl"></div>
          </div>
        </div>
        <div v-else>
          <p class="span-team"><span>77%</span> du projet réalisé à ce jour.</p>
          <div class="progress-bar__team">
            <div class="progress-bar-team__lvl"></div>
          </div>
        </div>
        <button @click="toggleProgress">
          {{ showSAEProgress ? 'Voir l\'avancée du projet' : 'Voir la temporalité du projet' }}
        </button>
      </div>
      <h2>QU'EST-CE QUE SPEEDDOCKER ?</h2>
      <p style="font-size: 14px;">SpeedDocker est un jeu d'arcade rapide et compétitif, conçu pour la borne de la
        formation MMI de l'IUT de
        Troyes. Inspiré du jeu SpeedRunners, il met en scène deux personnages emblématiques : la baleine de
        l'application
        Docker et Pat Gom. Le principe est simple : en solo ou en 1v1, vous devez survivre le plus longtemps possible en
        évitant les obstacles et grâce
        à des power-ups, et plus la partie dure, plus ça devient compliqué ! En 1v1, le premier à être hors-champ est
        éliminé !
        Avec ses mécaniques dynamiques et son rythme effréné, SpeedDocker promet des parties courtes mais intenses,
        idéales pour un environnement d'arcade.</p>
    </div>
  </div>

  <div class="fond-vide"></div>

  <Technologies />

  <div class="members">
    <h2>MEMBRES DU PROJET</h2>
    <ul class="members__list">
      <Member v-for="member in membersList" :key="member.name" :member="member" />
    </ul>
  </div>

  <div class="project">
    <div class="inaccessible">
      <p>à découvrir bientôt</p>
    </div>
    <h2>Découvrez un peu plus notre projet !</h2>
    <a href="">
      <i class="fa-brands fa-behance"></i>
      <span>Behance</span>
    </a>
  </div>

  <div class="burger">
    <i class="fa-solid fa-bars"></i>
  </div>

  <div class="infos">
    <ul class="menu">
      <h2 style="text-align:center; padding: 0; margin-bottom: 20px;">MENU</h2>
      <li><a href="#description" @click.prevent="setComponent('Description')"
          :class="{ active: currentComponent === 'Description' }">DESCRIPTION DU PROJET</a></li>
      <li><a href="#avancee" @click.prevent="setComponent('Avancee')"
          :class="{ active: currentComponent === 'Avancee' }">AVANCÉE DU PROJET</a></li>
      <li><a href="#note-cadrage" @click.prevent="setComponent('NoteCadrage')"
          :class="{ active: currentComponent === 'NoteCadrage' }">NOTE DE CADRAGE</a></li>
      <li><a href="#planning" @click.prevent="setComponent('Planning')"
          :class="{ active: currentComponent === 'Planning' }">PHASAGE / PLANNING</a></li>
      <li><a href="#art-domaine" @click.prevent="setComponent('EtatArtDomaine')"
          :class="{ active: currentComponent === 'EtatArtDomaine' }">ÉTAT DE L'ART DU DOMAINE</a></li>
    </ul>

    <div class="infos__projet" ref="infosProjet">
      <!-- If the window width is below 950px, display all components -->
      <Description v-if="currentComponent === 'Description' || shouldShowAllComponents" />
      <Avancee v-if="currentComponent === 'Avancee' || shouldShowAllComponents" />
      <NoteCadrage v-if="currentComponent === 'NoteCadrage' || shouldShowAllComponents" />
      <Planning v-if="currentComponent === 'Planning' || shouldShowAllComponents" />
      <EtatArtDomaine v-if="currentComponent === 'EtatArtDomaine' || shouldShowAllComponents" />
    </div>

    <News />

  </div>

  <footer>
    <p>© 2024-2025. Octo Studio - Tous droits réservés</p>
  </footer>
</template>

<style scoped>
.menu a.active {
  font-weight: bold;
  font-size: 15px;
  text-decoration: underline;
  text-underline-offset: 5px;
}
</style>
