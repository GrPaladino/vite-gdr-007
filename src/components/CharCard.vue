<script>
import { store } from "../store";

export default {
  data() {
    return {
      store,
    };
  },

  components: {},

  props: { character: [Object], flipImage: Boolean },

  methods: {},
};
</script>

<template>
  <div class="card h-100">
    <!--Nome del personaggio-->
    <h5 class="card-title mb-2 text-center mt-2">{{ character.name }}</h5>
    <div class="card-body d-flex">
      <div class="left me-2 w-50">
        <!--Descrizione personaggio-->
        <p class="card-text">
          <strong>Defence: </strong>
          {{ character.defence }}
        </p>
        <p class="card-text">
          <strong>Intelligence: </strong>
          {{ character.intelligence }}
        </p>
        <p class="card-text">
          <strong>HP: </strong>
          {{ character.life }}
        </p>
        <p class="card-text">
          <strong>Speed: </strong>
          {{ character.speed }}
        </p>
        <p class="card-text">
          <strong>Strength: </strong>
          {{ character.strength }}
        </p>
      </div>

      <div class="right w-50">
        <p class="text-center fs-4">
          <strong>{{ character.type.name }}</strong>
        </p>
        <div :class="flipImage ? 'flip' : ''">
          <img
            :src="character.type.img"
            alt=""
            class="img-thumbnail border-0" />
        </div>
      </div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "../style/partials/mixins" as *;
@use "../style/partials/variables" as *;

.card {
  width: 70%;
  margin: 0 auto;
  opacity: 0.8;
  border-radius: 10px;

  .flip {
    transform: scaleX(-1);
  }
}
</style>
