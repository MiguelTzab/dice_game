<template>
  <v-card class="mx-auto w-100" elevation="2">
    <v-list-item three-line>
      <v-list-item-content>
        <v-hover v-slot="{ hover }" :disabled="disabled">
          <v-list-item-title class="title mb-1">
            {{ player.name }}
            <v-list-item-icon v-if="hover">
              <v-btn icon @click="onRemovePlayer">
                <v-icon color="red">
                  mdi-minus-circle
                </v-icon>
              </v-btn>
            </v-list-item-icon>
            <v-list-item-icon v-else>
              <v-icon :color="player.turn ? 'blue darken-1 accent-4' : 'grey'">
                mdi-dice-5
              </v-icon>
            </v-list-item-icon>
          </v-list-item-title>
        </v-hover>
        <div class="d-flex">
          <v-list-item-subtitle class="text-center">
            <div class="subtitle-2">Actual</div>
            <div class="caption">{{ player.score }}</div>
          </v-list-item-subtitle>
          <v-list-item-subtitle class="text-center">
            <div class="subtitle-2">Total</div>
            <div class="caption">{{ player.globlaScore }}</div>
          </v-list-item-subtitle>
        </div>
      </v-list-item-content>
    </v-list-item>
  </v-card>
</template>

<script>
export default {
  name: "Player",
  props: {
    player: Object,
    disabled: Boolean,
  },
  data: () => ({}),
  methods: {
    onRemovePlayer() {
      this.$emit("remove", this.player.name);
    },
  },
};
</script>
