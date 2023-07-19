<script>
import { store } from "../store";
export default {
  data() {
    return {
      store,
    };
  },
  props: {
    dataCard: Object,
  },
  methods: {
    formatDate(date) {
      const parts = date.split("-");
      const formattedDate = `${parts[2]}-${parts[1]}-${parts[0]}`;
      return formattedDate;
    },
  },
};
</script>

<template>
  <div class="col">
    <div class="content">
      <div class="card_project col-3">
        <!-- controllo se l'immagine esiste -->
        <img
          style="width: 300px"
          :src="this.store.baseUrl + 'storage/' + dataCard.image"
          :alt="dataCard.title"
        />
        <div class="title">{{ dataCard.title }}</div>
        <div class="author">{{ dataCard.author }}</div>
        <div class="creation_date">
          {{ formatDate(dataCard.creation_date) }}
        </div>
        <div class="last_update">{{ formatDate(dataCard.last_update) }}</div>
        <div v-if="dataCard.collaborators" class="collaborators">
          {{ dataCard.collaborators }}
        </div>
        <div v-if="dataCard.description" class="description">
          {{ dataCard.description }}
        </div>
        <div class="link_github">{{ dataCard.link_github }}</div>
        <div class="type">{{ dataCard.type.name }}</div>
        <div class="languages">
          <span v-for="languages in dataCard.languages">
            {{ languages.name }},
          </span>
        </div>
        <router-link
          :to="{ name: 'projects.show', params: { slug: dataCard.slug } }"
          >View</router-link
        >
      </div>
      <!-- <div class="card">
        <div class="circle"></div>
        <div class="circle"></div>
        <div class="card-inner">
          <img
            style="height: 100%; width: 100%; object-fit: cover"
            :src="this.store.baseUrl + 'storage/' + dataCard.image"
            :alt="dataCard.image"
          />
        </div>
      </div> -->
    </div>
  </div>
</template>

<style scoped>
/* .card {
  width: 209px;
  height: 279.4px;
  transition: all 0.2s;
  position: relative;
  cursor: pointer;
  margin: 2rem 0;
}

.card-inner {
  width: inherit;
  height: inherit;
  background: rgba(255, 255, 255, 0.05);
  box-shadow: 0 0 10px rgba(0, 0, 0, 0.25);
  backdrop-filter: blur(10px);
  border-radius: 8px;
  padding: 1rem;
}

.card:hover {
  transform: scale(1.04) rotate(1deg);
}

.circle {
  width: 100px;
  height: 100px;
  background: radial-gradient(#b0e633, #53ef7d);
  border-radius: 50%;
  position: absolute;
  animation: move-up6 2s ease-in infinite alternate-reverse;
}

.circle:nth-child(1) {
  top: -25px;
  left: -25px;
}

.circle:nth-child(2) {
  bottom: -25px;
  right: -25px;
  animation-name: move-down1;
}

@keyframes move-up6 {
  to {
    transform: translateY(-10px);
  }
}

@keyframes move-down1 {
  to {
    transform: translateY(10px);
  }
} */
</style>
