<script>
import axios from "axios";

import CardProject from "./CardProject.vue";
export default {
  data() {
    return {
      arrProjects: [],
      arrTypes: [],
      currentPage: 1,
      nPages: 0,
      firstPage: false,
      lastPage: false,
      loader: true,
    };
  },
  methods: {
    changePage(page) {
      this.currentPage = page;
      // this.getProjects();
      this.firstPage = !this.firstPage;
      this.lastPage = !this.lastPage;
    },
    nextPage() {
      this.currentPage++;
      // this.getProjects();
      if (this.currentPage >= this.nPages) {
        this.lastPage = true;
      }
      this.firstPage = false;
    },
    previousPage() {
      this.currentPage--;
      // this.getProjects();
      if (this.currentPage <= 1) {
        this.firstPage = true;
      }
      this.lastPage = false;
    },
    getTypes() {
      axios.get("http://localhost:8000/api/types").then((response) => {
        this.arrTypes = response.data.results;
      });
    },
    getProjects() {
      this.loader = true;
      axios
        .get("http://localhost:8000/api/projects", {
          params: {
            page: this.currentPage,
            // se sto già in prjects.index non esegue il craeated e non aggiorna la pagina
            q: new URLSearchParams(window.location.search).get("q"),
          },
        })
        .then((response) => {
          this.arrProjects = response.data.results.data;
          this.nPages = response.data.results.last_page;
          this.loader = false;
        });
    },
  },
  created() {
    this.getTypes();
    this.getProjects();
  },
  watch: {
    currentPage() {
      this.getProjects();
    },
  },
  components: { CardProject },
};
</script>

<template>
  <div class="container">
    <form>
      <label class="mb-2" for="type">Type</label>
      <select class="form-select w-25" id="type">
        <option v-for="type in arrTypes" :key="type.id" :value="type.id">
          {{ type.name }}
        </option>
      </select>
    </form>
    {{ loader }}
    <div v-if="!loader" class="row row-cols-3 my-5">
      <CardProject
        v-for="project in arrProjects"
        :key="project.id"
        :dataCard="project"
      />
    </div>
    <div v-else>
      caricamento
      <!-- caricamento in corso  -->
    </div>

    <nav>
      <ul class="pagination">
        <li class="page-item">
          <button
            class="page-link"
            :class="{ disabled: firstPage }"
            @click="previousPage()"
          >
            Previous
          </button>
        </li>

        <li
          v-for="page in nPages"
          :key="page"
          class="page-item num_pages"
          :class="{ active: page == currentPage }"
        >
          <span class="page-link" @click="changePage(page)">
            {{ page }}
          </span>
        </li>

        <li class="page-item">
          <button
            class="page-link"
            :class="{ disabled: lastPage }"
            @click="nextPage()"
          >
            Next
          </button>
        </li>
      </ul>
    </nav>
  </div>
</template>

<style lang="scss" scoped>
.num_pages {
  cursor: pointer;
}
</style>
