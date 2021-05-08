<template>
  <v-dialog v-model="dialog" persistent max-width="490">
    <v-card>
      <div class="d-flex flex-no-wrap justify-space-between">
        <div>
          <v-card-title class="text-h5">Fin del juego</v-card-title>

          <v-card-subtitle>Ganador: {{ winner }}</v-card-subtitle>
        </div>

        <v-avatar class="ma-3" size="155" tile>
          <v-img
            src="https://acegif.com/wp-content/gif/confetti-25.gif"
          ></v-img>
        </v-avatar>
      </div>
      <v-card-actions>
        <v-btn outlined rounded text @click="reset">
          Aceptar
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "Winner",
  props: {
    winner: String,
  },
  data: () => ({
    dialog: true,
  }),
  methods: {
    reset() {
      location.reload();
    },
  },
};
</script>

<style></style>
