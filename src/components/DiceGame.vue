<template>
  <v-container fluid id="game">
    <v-row class="text-center">
      <v-col cols="12">
        <v-card class="mx-auto mt-3">
          <v-card-text>
            <v-container fluid>
              <v-row>
                <v-col cols="2">
                  <players-list
                    :players="players"
                    :disabled="playing"
                    @hasPlayers="(val) => (hasPlayers = val)"
                    @addPlayer="onAddPlayer"
                    @removePlayer="onRemovePlayer"
                  />
                </v-col>
                <v-col cols="10">
                  <dices-list
                    :dices="dices"
                    :disabled="playing"
                    @addDice="onAddDice"
                    @removeDice="onRemoveDice"
                    :rolling="rolling"
                  />
                </v-col>
              </v-row>
            </v-container>
          </v-card-text>
          <v-fab-transition v-if="canRollDices">
            <v-tooltip top>
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  color="primary"
                  fab
                  large
                  class="play-btn"
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
          <v-fab-transition v-else>
            <v-tooltip top>
              <template v-slot:activator="{ on, attrs }">
                <v-btn
                  color="primary"
                  fab
                  large
                  class="play-btn"
                  v-bind="attrs"
                  :disabled="!canStart"
                  v-on="on"
                  @click="onStart"
                >
                  <v-icon>mdi-play</v-icon>
                </v-btn>
              </template>
              <span>Play</span>
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
          <instructions />
          <add-turns v-if="showTurnsForm" @save="onSaveTurn" />
          <winner v-if="showWinner" :winner="winner.name" />
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import DicesList from "./DicesList.vue";
import PlayersList from "./PlayersList";
import Instructions from "./modals/Instructions";
import AddTurns from "./modals/AddTurns";
import Winner from "./modals/Winner";

export default {
  components: { PlayersList, DicesList, Instructions, AddTurns, Winner },
  name: "DiceGame",
  data: () => ({
    currentTurn: 0,
    numTurns: null,
    hasPlayers: false,
    showSnackbar: false,
    showTurnsForm: false,
    showWinner: false,
    rolling: false,
    winner: undefined,
    playing: false,
    players: [],
    dices: [],
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
    onAddDice(sides) {
      this.dices.push({
        sides: sides,
        side_number: 0,
      });
    },
    onRemoveDice(index) {
      this.dices.splice(index, 1);
    },
    onSaveTurn(turn) {
      this.numTurns = turn;
      this.playing = true;
      this.onCancelTurn();
    },
    onCancelTurn() {
      this.showTurnsForm = false;
    },
    async onRoll() {
      this.rolling = true;
      let sumSides = 0;
      this.dices.forEach((dice) => {
        const side_number = this.getNextSide(dice.sides, dice.side_number);
        dice.side_number = side_number;
        sumSides += side_number;
        return dice;
      });
      const playerIndex = this.players.findIndex(
        (player) => player.turn == true
      );
      //make time for transition
      await this.waitAnimation();
      this.rolling = false;

      this.players[playerIndex].score = sumSides;
      this.players[playerIndex].globlaScore += sumSides;

      this.currentTurn = this.getNextTurn(this.currentTurn);
    },
    waitAnimation() {
      return new Promise(function(resolve) {
        setTimeout(resolve, 1000);
      });
    },
    gameOver() {
      const winner = this.players
        .map((player) => player)
        .sort((a, b) => a.globlaScore - b.globlaScore);
      this.winner = winner[winner.length - 1];
      this.showWinner = true;
    },
    onStart() {
      this.showTurnsForm = true;
    },
    getNextTurn(turn) {
      if (turn == this.players.length - 1) {
        this.numTurns -= 1;
        return 0;
      } else return turn + 1;
    },
    getNextSide(numSides, oldSide) {
      let side = null;
      do {
        side = this.getRandom(numSides);
      } while (side == oldSide);
      return side;
    },
    getRandom(max) {
      max = Math.floor(max);
      return Math.floor(Math.random() * (max - 1 + 1)) + 1;
    },
  },
  computed: {
    canRollDices() {
      return this.canStart && this.playing;
    },
    canStart() {
      return this.players.length > 0 && this.dices.length > 0;
    },
  },
  watch: {
    currentTurn: function(newTurn, oldTurn) {
      this.players[oldTurn].turn = false;
      this.players[newTurn].turn = true;
    },
    numTurns: function(newTurn) {
      if (newTurn == 0) this.gameOver();
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
