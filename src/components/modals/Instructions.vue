<template>
  <v-dialog v-model="dialog" persistent max-width="490">
    <v-card>
      <v-card-title class="headline">
        Bienvenido
      </v-card-title>
      <v-card-text>
        Hola, para poder comenzar hay que agregar a los jugadores y los dados
        que se usaran en la partida, una vez completado esto puedes darle click
        al botón de play
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="green" text @click="dialog = false">
          Aceptar
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "Instructions",
  data: () => ({
    dialog: true,
  }),
};
</script>

<style></style>
