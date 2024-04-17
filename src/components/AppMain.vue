<script>
// import { store } from "../store";
import axios from "axios";

export default {
  data() {
    return {
      characters: [],
    };
  },

  components: {},

  methods: {
    fetchCharacters() {
      axios.get("http://127.0.0.1:8000/api/characters").then((response) => {
        this.characters = response.data.characters;
      });
    },
  },

  created() {
    this.fetchCharacters();
  },
};
</script>

<template></template>

<style lang="scss" scoped>
@use "../style/partials/mixins" as *;
@use "../style/partials/variables" as *;
</style>
