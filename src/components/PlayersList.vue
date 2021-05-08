<template>
  <v-virtual-scroll :items="list" :item-height="140" height="400">
    <template v-slot:default="{ item }">
      <v-list-item>
        <Player :player="item" />
      </v-list-item>
    </template>
  </v-virtual-scroll>
</template>

<script>
import Player from "./Player";
export default {
  components: {
    Player,
  },
  props: {
    list: Array,
  },
  name: "PlayersList",
  data: () => ({}),
};
</script>
