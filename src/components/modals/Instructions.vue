<template>
  <v-dialog v-model="dialog" persistent max-width="490">
    <v-card>
      <v-card-title class="headline">
        Hola, Bienvenido
      </v-card-title>
      <v-card-text>
        <p class="subtitle-2">Para iniciar el juego realiza lo siguiente:</p>
        <br />
        <ol class="ml-4">
          <li>Agrega a los jugadores</li>
          <li>Agrega dados por su número de caras</li>
          <li>
            Picale al botón de 'play'
          </li>
          <li>
            Elige el número de tiros por jugador
          </li>
        </ol>
        <br />
        <small>Si quieres reiniciar el juego, recarga la página</small>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="primary" text @click="dialog = false">
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
