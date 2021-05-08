<template>
  <div>
    <v-card class="pa-2 grey lighten-5" elevation="0">
      <v-toolbar>
        <v-toolbar-title>Dados</v-toolbar-title>
        <v-fab-transition>
          <v-btn
            color="primary"
            fab
            small
            absolute
            bottom
            right
            :disabled="disabled"
            @click="onAddDice"
          >
            <v-icon>mdi-plus</v-icon>
          </v-btn>
        </v-fab-transition>
      </v-toolbar>
      <v-card-text>
        <v-item-group>
          <v-fade-transition>
            <v-row v-if="!rolling">
              <v-col md="2" v-for="(item, i) in dices" :key="i">
                <v-item>
                  <dice
                    :dice="item"
                    :disabled="disabled"
                    @remove="onRemoveDice(i)"
                  />
                </v-item>
              </v-col>
            </v-row>
          </v-fade-transition>
        </v-item-group>
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
    disabled: Boolean,
    rolling: Boolean,
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
