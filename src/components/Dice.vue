<template>
  <v-card class="mx-auto dice">
    <v-hover v-slot="{ hover }" :disabled="disabled">
      <v-card-text>
        <h1 class="dice-side-title">{{ dice.side_number }}</h1>
        <v-icon class="mr-1">
          mdi-dice-3
        </v-icon>
        <span class="subheading mr-2">{{ dice.sides }}</span>
        <v-btn icon @click="onRemoveDice" v-if="hover">
          <v-icon color="red">
            mdi-minus-circle
          </v-icon>
        </v-btn>
      </v-card-text>
    </v-hover>
  </v-card>
</template>

<script>
export default {
  name: "Dice",
  props: {
    dice: Object,
    disabled: Boolean,
  },
  data: () => ({}),
  methods: {
    onRemoveDice() {
      this.$emit("remove");
    },
  },
};
</script>

<style scoped>
.dice {
  width: 8rem;
  height: 8rem;
}
.dice-side-title {
  font-size: 4rem;
  line-height: initial;
}
</style>
