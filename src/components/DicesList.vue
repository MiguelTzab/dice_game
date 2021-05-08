<template>
  <div>
    <v-card class="pa-2 grey lighten-5" elevation="0">
      <v-toolbar>
        <v-toolbar-title>Dados</v-toolbar-title>
        <v-fab-transition>
          <v-btn fab dark small absolute bottom right @click="onAddDice">
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-fab-transition>
      </v-toolbar>
      <v-card-text>
        <v-virtual-scroll
          :items="dices"
          :item-height="140"
          height="400"
          class="mt-3"
        >
          <template v-slot:default="{ item, index }">
            <v-list-item>
              <dice :dice="item" @remove="onRemoveDice(index)" />
            </v-list-item>
          </template>
        </v-virtual-scroll>
      </v-card-text>
    </v-card>
    <add-dice
      v-if="showDiceForm"
      @cancel="onCancelAddDice"
      @save="onSaveDice"
    />
  </div>
</template>

<script>
import Dice from "./Dice";
import AddDice from "./modals/AddDice";

export default {
  name: "DicesList",
  components: {
    Dice,
    AddDice,
  },
  props: {
    dices: Array,
  },
  data: () => ({
    showDiceForm: false,
  }),
  methods: {
    onAddDice() {
      this.showDiceForm = true;
    },
    onCancelAddDice() {
      this.showDiceForm = false;
    },
    onSaveDice(sides) {
      this.$emit("addDice", sides);
      this.onCancelAddDice();
    },
    onRemoveDice(index) {
      this.$emit("removeDice", index);
    },
  },
};
</script>
