<script>
export default {
  data() {
    return {
      searchStr: "",
    };
  },
  //TODO pulire il campo di ricerca
  // updated() {
  //   this.searchStr = new URLSearchParams(window.location.search).get('q');
  // }
};
</script>

<template>
  <nav>
    <div class="container">
      <div class="row">
        <div class="content">
          <ul class="d-flex gap-3 py-4 list-unstyled">
            <li>
              <router-link class="navbar-brand" :to="{ name: 'home' }"
                >Boolpress</router-link
              >
            </li>
            <li>
              <router-link class="nav-item" :to="{ name: 'about' }"
                >About</router-link
              >
            </li>
            <li>
              <router-link class="nav-item" :to="{ name: 'projects.index' }"
                >Projects</router-link
              >
            </li>
            <li>
              <form
                class="d-flex"
                role="search"
                @submit.prevent="
                  $router.push({
                    name: 'projects.index',
                    query: { q: searchStr },
                  })
                "
              >
                <input
                  class="form-control me-2"
                  type="search"
                  placeholder="Search"
                  aria-label="Search"
                  name="q"
                  v-model="searchStr"
                />
                <button class="btn btn-outline-success" type="submit">
                  Search
                </button>
              </form>
            </li>
          </ul>
        </div>
      </div>
    </div>
  </nav>
</template>

<style></style>
