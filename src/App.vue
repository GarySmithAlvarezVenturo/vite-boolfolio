<script>
import axios from "axios";
import AppNav from "./components/AppNav.vue";
import AppFooter from "./components/AppFooter.vue";
export default {
  components: {
    AppNav,
    AppFooter,
  },
  // richiesta per i dati del post
  // created() {
  //   axios.get(this.store.baseUrl + 'projects/' + this.$route.params.slag)
  // }
};
</script>

<template>
  <AppNav />
  <router-view></router-view>
  <AppFooter />
</template>

<style lang="scss">
@import "bootstrap/scss/bootstrap";
</style>
