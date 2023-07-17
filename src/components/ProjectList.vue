<script>
import axios from "axios";

import CardProject from "./CardProject.vue";
export default {
  data() {
    return {
      arrProjects: [],
      currentPage: 1,
      nPages: 0,
      firstPage: false,
      lastPage: false,
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
    getProjects() {
      axios
        .get("http://localhost:8000/api/projects", {
          params: {
            page: this.currentPage,
          },
        })
        .then((response) => {
          this.arrProjects = response.data.data;
          this.nPages = response.data.last_page;
        });
    },
  },
  created() {
    axios
      .get("http://localhost:8000/api/projects", {
        params: {
          page: this.nPage,
        },
      })
      .then((response) => {
        this.arrProjects = response.data.data;
        this.nPages = response.data.last_page;
      });
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
    <h1 class="text-danger">Boolpress</h1>
    <div class="row row-cols-3">
      <CardProject
        v-for="project in arrProjects"
        :key="project.id"
        :dataCard="project"
      />
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
