<template>
  <v-container fluid id="game">
    <v-row class="text-center">
      <v-col cols="12">
        <v-card class="mx-auto mt-3">
          <v-card-text>
            <players-list
              :players="players"
              @hasPlayers="(val) => (hasPlayers = val)"
              @addPlayer="onAddPlayer"
              @removePlayer="onRemovePlayer"
            />
          </v-card-text>
          <v-fab-transition>
            <v-tooltip top>
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  fab
                  large
                  dark
                  class="play-btn"
                  :disabled="!canRollDices"
                  v-bind="attrs"
                  v-on="on"
                  @click="onRoll"
                >
                  <v-icon>mdi-dice-multiple-outline</v-icon>
                </v-btn>
              </template>
              <span>Lanzar dados</span>
            </v-tooltip>
          </v-fab-transition>
          <v-snackbar
            v-model="showSnackbar"
            absolute
            top
            right
            color="blue darken-3"
          >
            {{ message }}
          </v-snackbar>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import PlayersList from "./PlayersList";
export default {
  components: { PlayersList },
  name: "DiceGame",
  data: () => ({
    players: [],
    hasPlayers: false,
    showSnackbar: false,
    currentTurn: 0,
    message: "",
  }),
  methods: {
    onAddPlayer(name) {
      const nameAlreadyExists = this.players.some(
        (player) => player.name == name
      );
      if (!nameAlreadyExists)
        this.players.push({
          turn: this.players.length == 0,
          name,
          score: 0,
          globlaScore: 0,
        });
      else {
        this.message = "El nombre ya existe en la lista";
        this.showSnackbar = true;
      }
    },
    onRemovePlayer(name) {
      this.players = this.players.filter((player) => player.name != name);
      this.players.map((player, index) => {
        player.turn = index == 0;
        return player;
      });
    },
    onRoll() {
      this.currentTurn = this.getNextTurn(this.currentTurn);
    },
    getNextTurn(turn) {
      if (turn == this.players.length - 1) return 0;
      else return turn + 1;
    },
  },
  computed: {
    canRollDices() {
      return this.players.length > 0;
    },
  },
  watch: {
    currentTurn: function(newTurn, oldTurn) {
      this.players[oldTurn].turn = false;
      this.players[newTurn].turn = true;
    },
  },
};
</script>

<style scoped>
#game .play-btn {
  bottom: 2rem;
  right: 3rem;
  position: absolute;
  margin: 0 0 16px 16px;
}
</style>
