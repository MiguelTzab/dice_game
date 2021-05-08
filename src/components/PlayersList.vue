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
            <v-virtual-scroll
              :items="players"
              :item-height="140"
              height="400"
              class="mt-3"
            >
              <template v-slot:default="{ item }">
                <v-list-item>
                  <Player :player="item" @remove="onRemovePlayer" />
                </v-list-item>
              </template>
            </v-virtual-scroll>
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
import Player from "./Player";
import AddPlayer from "./modals/AddPlayer";

export default {
  name: "PlayersList",
  components: {
    Player,
    AddPlayer,
  },
  props: {
    players: Array,
  },
  data: () => ({
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
      this.$emit("addPlayer", name);
      this.onCancelAddPlayer();
    },
    onRemovePlayer(name) {
      this.$emit("removePlayer", name);
    },
  },
};
</script>
