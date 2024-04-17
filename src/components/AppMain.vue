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
  },

  components: {},

  methods: {
    fetchcharacters() {
      axios.get("http://127.0.0.1:8000/api/characters").then((response) => {
        store.characters = response.data.characters;
      });
    },
  },

  created() {
    this.fetchcharacters();
  },
};
</script>

<template></template>

<style lang="scss" scoped>
@use "../style/partials/mixins" as *;
@use "../style/partials/variables" as *;
</style>
