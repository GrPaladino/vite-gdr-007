<script>
import { store } from "../store";
import CharCard from "./CharCard.vue";
// IMPORTA AXIOS
// import { store } from "../store";
import axios from "axios";

export default {
  data() {
    return {
      store,
      isSelected: false,
    };
      characters: [],
    };
  },

  components: {
  },

  methods: {
  },
};
</script>

<template></template>

<style lang="scss" scoped>
@use "../style/partials/mixins" as *;
@use "../style/partials/variables" as *;
</style>
