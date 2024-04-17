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

<template>
  <div class="container mt-5">
    <label for="characters"><b class="fs-4">Choose a character:</b></label>
    <select class="form-select" name="characters" id="characters">
      <option v-for="charact in store.characters" :value="charact.id">
        {{ charact.name }}
      </option>
      <!-- <option value="2">Elena</option>
      <option value="3">Gareth</option>
      <option value="4">Sylvia</option>
      <option value="5">Liam</option>
      <option value="6">Isabella</option>
      <option value="7">Oscar</option>
      <option value="8">Aria</option>
      <option value="9">Victor</option>
      <option value="10">Luna</option>
      <option value="11">Xander</option>
      <option value="12">Sophia</option>
      <option value="13">Maximus</option> -->
    </select>
    <div class="row mt-5">
      <div class="col">
        <char-card />
      </div>
      <div class="col">
        <char-card />
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "../style/partials/mixins" as *;
@use "../style/partials/variables" as *;
</style>
