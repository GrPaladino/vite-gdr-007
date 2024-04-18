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
      isWin: false,
      isDefeat: false,
      isEven: false,
      selectValue: -1,
      mainCharacter: "",
      computerCharacter: "",
      computerHP: "",
      mainCharacterHP: "",
      CpuAttack: false,
      flipImage: true,
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
        this.isWin = false;
        this.isDefeat = false;
        this.isEven = false;
      }
    },

    getRandomInt(min, max) {
      const minCeiled = Math.ceil(min);
      const maxFloored = Math.floor(max);
      return Math.floor(Math.random() * (maxFloored - minCeiled) + minCeiled);
    },

    fetchOpponentCharacter() {
      let randNumber = this.getRandomInt(0, 12);
      if (randNumber === this.mainCharacter.id - 1) {
        randNumber = this.getRandomInt(0, 12);
      }
      this.computerCharacter = store.characters[randNumber];
    },

    fetchWinner() {
      let ourStrength = this.mainCharacter.strength;
      let computerDefence = this.computerCharacter.defence;

      if (ourStrength > computerDefence) {
        this.iswin = true;
      } else if (ourStrength < computerDefence) {
        this.isdefeat = true;
      } else {
        this.isEven = true;
      }
    },

    fetchAttack() {
      this.computerHP = this.computerCharacter.life;

      const mainStrength = this.mainCharacter.strength;
      const computerDefence = this.computerCharacter.defence;

      const difference = mainStrength - computerDefence;

      if (mainStrength > computerDefence) {
        this.computerHP = this.computerHP - difference;
        this.computerCharacter.life = this.computerHP;
      } else {
        const negativeDifference = computerDefence - mainStrength;
        this.mainCharacter.life = this.mainCharacter.life - negativeDifference;
      }

      if (this.computerCharacter.life <= 0) {
        this.isWin = true;
        this.computerCharacter.life = 0;
      }
      if (this.mainCharacter.life <= 0) {
        this.isDefeat = true;
        this.mainCharacter.life = 0;
      }

      setTimeout(() => {
        this.cpuAttackTrue();
      }, 1000);

      setTimeout(() => {
        this.fetchComputerAttack();
      }, 2000);
    },

    fetchComputerAttack() {
      this.mainCharacterHP = this.mainCharacter.life;

      const mainDefence = this.mainCharacter.defence;
      const computerAttack = this.computerCharacter.strength;
      const difference = computerAttack - mainDefence;

      if (computerAttack > mainDefence) {
        this.mainCharacterHP = this.mainCharacterHP - difference;
        this.mainCharacter.life = this.mainCharacterHP;
      } else {
        const negativeDifference = mainDefence - computerAttack;
        this.computerCharacter.life =
          this.computerCharacter.life - negativeDifference;
      }

      if (this.mainCharacter.life <= 0) {
        this.isDefeat = true;
        this.mainCharacter.life = 0;
      }
      if (this.computerCharacter.life <= 0) {
        this.isWin = true;
        this.computerCharacter.life = 0;
      }

      setTimeout(() => {
        this.cpuAttackReturnFalse();
      }, 1000);
    },

    cpuAttackReturnFalse() {
      this.CpuAttack = false;
    },

    cpuAttackTrue() {
      this.CpuAttack = true;
    },
  },

  created() {
    this.fetchcharacters();
  },
};
</script>

<template>
  <div class="container mt-5 py-4">
    <!-- <label for="characters"
      ><b class="fs-2 mb-5 text-light">Choose a character:</b></label
    > -->
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
        <char-card
          v-if="mainCharacter"
          :character="mainCharacter"
          :flipImage="flipImage" />
      </div>
      <div class="col-6">
        <char-card v-if="computerCharacter" :character="computerCharacter" />
      </div>
    </div>
    <div class="d-flex justify-content-around mt-4">
      <button
        @click="fetchAttack()"
        v-if="mainCharacter && !CpuAttack && !isWin && !isDefeat"
        class="btn btn-success text-center mt-4">
        Play
      </button>
      <h3
        v-if="mainCharacter && CpuAttack && !isWin && !isDefeat"
        class="text-center p-2">
        CPU Attacking
      </h3>
    </div>
    <div class="result d-flex justify-content-center mt-4">
      <h2 v-if="isWin" class="text-success">You Won!!</h2>
      <h2 v-if="isDefeat" class="text-danger">GAME OVER</h2>
      <h2 v-if="isEven" class="text-primary">Even, try again!!!!</h2>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "../style/partials/mixins" as *;
@use "../style/partials/variables" as *;

.container {
  height: 90vh;
  background-image: url("../../img/Street-Fighter-Duel-1.jpg");
  background-repeat: no-repeat;
  background-size: cover;

  select {
    opacity: 0.8;
  }

  .result,
  h3 {
    width: 400px;
    margin: 50px auto;
    background-color: white;
    opacity: 0.8;
    border-radius: 10px;
  }

  button {
    width: 200px;
  }
}
</style>
