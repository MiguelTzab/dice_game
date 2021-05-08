<template>
  <v-app>
    <v-app-bar app color="primary" dark>
      <div class="d-flex align-center">
        <h1 class="display-1">Dice Game</h1>
      </div>
      <v-spacer></v-spacer>
      <v-icon large>
        mdi-dice-6
      </v-icon>
    </v-app-bar>

    <v-main>
      <dice-game />
    </v-main>
  </v-app>
</template>

<script>
import DiceGame from "./components/DiceGame";

export default {
  name: "App",

  components: {
    DiceGame,
  },

  data: () => ({
    //
  }),
};
</script>

<style>
.w-100 {
  width: 100%;
}
.h-100 {
  height: 100%;
}
</style>
