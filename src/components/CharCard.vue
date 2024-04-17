<script>
import { store } from "../store";

export default {
  data() {
    return {
      store,
    };
  },

  components: {},

  //   props: { randomChar },

  methods: {},
};
</script>

<template>
  <div class="card" style="width: 18rem">
    <!-- <img src="..." class="card-img-top" alt="..." /> -->
    <div class="card-body">
      <!--Nome del personaggio-->
      <h5 class="card-title">Card title</h5>
      <!--Descrizione personaggio-->
      <p class="card-text">
        Some quick example text to build on the card title and make up the bulk
        of the card's content.
      </p>
      <!-- Conferma scelta -->
      <a href="#" class="btn btn-primary">Go somewhere</a>
    </div>
  </div>
</template>

<style lang="scss" scoped>
@use "../style/partials/mixins" as *;
@use "../style/partials/variables" as *;
</style>
