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
      iswin: false,
      isdefeat: false,
      isEven: false,
      selectValue: -1,
      mainCharacter: "",
      computerCharacter: "",
    };
  },

  components: { CharCard },

  methods: {
    fetchcharacters() {
      axios.get("http://127.0.0.1:8000/api/characters").then((response) => {
        store.characters = response.data.characters;
      });
    },

    fetchMainCharacter() {
      if (this.selectValue != -1) {
        this.mainCharacter = store.characters[this.selectValue];
      }
    },

    getRandomInt(min, max) {
      const minCeiled = Math.ceil(min);
      const maxFloored = Math.floor(max);
      return Math.floor(Math.random() * (maxFloored - minCeiled) + minCeiled);
    },

    fetchOpponentCharacter() {
      let randNumber = this.getRandomInt(0, 12);
      this.computerCharacter = store.characters[randNumber];
    },

    fetchWinner() {
      let ourStrength = this.mainCharacter.strength;
      let computerDefence = this.computerCharacter.defence;
      this.iswin = false;
      this.isdefeat = false;
      this.isEven = false;

      if (ourStrength > computerDefence) {
        this.iswin = true;
      } else if (ourStrength < computerDefence) {
        this.isdefeat = true;
      } else {
        this.isEven = true;
      }
    },
  },

  created() {
    this.fetchcharacters();
  },
};
</script>

<template>
  <div class="container mt-5">
    <label for="characters"><b class="fs-4 mb-5">Choose a character:</b></label>
    <select
      class="form-select mt-2"
      name="characters"
      id="characters"
      @change="fetchMainCharacter(), fetchOpponentCharacter()"
      v-model="selectValue">
      <option value="-1">Choose a character</option>
      <option v-for="(charact, index) in store.characters" :value="index">
        {{ charact.name }}
      </option>
    </select>
    <div class="row mt-5">
      <div class="col-6">
        <char-card v-if="mainCharacter" :character="mainCharacter" />
      </div>
      <div class="col-6">
        <char-card v-if="computerCharacter" :character="computerCharacter" />
      </div>
    </div>
    <div class="d-flex justify-content-center mt-4">
      <button
        @click="fetchWinner()"
        v-if="mainCharacter"
        class="btn btn-success text-center">
        Play
      </button>
    </div>
    <div class="result d-flex justify-content-center mt-4">
      <h2 v-if="iswin" class="text-success">You Won!!</h2>
      <h2 v-if="isdefeat" class="text-danger">You Lost, try again!!!!!!!!</h2>
      <h2 v-if="isEven" class="text-primary">Even, try again!!!!</h2>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "../style/partials/mixins" as *;
@use "../style/partials/variables" as *;
</style>
