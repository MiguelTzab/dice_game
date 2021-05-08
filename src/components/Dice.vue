<template>
  <v-card class="mx-auto dice">
    <v-card-text>
      <h1 class="dice-side-title">{{ dice.side_number }}</h1>
      <v-icon class="mr-1">
        mdi-dice-3
      </v-icon>
      <span class="subheading mr-2">{{ dice.sides }}</span>
    </v-card-text>
  </v-card>
</template>

<script>
export default {
  name: "Dice",
  props: {
    dice: Object,
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
