<script>
// Global state store
// import { store } from "./store";

// Import components
import AppHeader from "./components/AppHeader.vue";
import AppMain from "./components/AppMain.vue";
import AppFooter from "./components/AppFooter.vue";

export default {
  data() {
    return {
      // store,
    };
  },

  components: {
    AppHeader,
    AppMain,
    AppFooter,
  },
};
</script>

<template>
  <app-header />
  <app-main />
  <app-footer />
</template>

<style lang="scss">
@use "./style/general.scss";
</style>
