<template>
  <v-container fluid>
    <v-row no-gutters>
      <v-col class="col-md-2">
        <v-card class="pa-2" elevation="0">
          <v-toolbar>
            <v-toolbar-title>Jugadores</v-toolbar-title>
            <v-fab-transition>
              <v-btn fab dark small absolute bottom right @click="onAddPlayer">
                <v-icon>mdi-plus</v-icon>
              </v-btn>
            </v-fab-transition>
          </v-toolbar>
          <v-card-text>
            <players-list :list="players" class="mt-3" />
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <add-player
      v-if="showPlayerForm"
      @cancel="onCancelAddPlayer"
      @save="onSavePlayer"
    />
  </v-container>
</template>

<script>
import PlayersList from "./PlayersList";
import AddPlayer from "./modals/AddPlayer";
export default {
  components: { PlayersList, AddPlayer },
  name: "SideBar",
  data: () => ({
    players: [],
    nextKey: 1,
    showPlayerForm: false,
  }),
  methods: {
    onAddPlayer() {
      this.showPlayerForm = true;
    },
    onCancelAddPlayer() {
      this.showPlayerForm = false;
    },
    onSavePlayer(name) {
      const key = this.nextKey++;
      this.players.push({
        key,
        turn: key == 1,
        name,
        score: 0,
        globlaScore: 0,
      });
      this.onCancelAddPlayer();
    },
  },
};
</script>

<style></style>
