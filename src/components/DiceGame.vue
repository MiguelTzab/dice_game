<template>
  <v-container fluid>
    <v-row class="text-center">
      <v-col cols="12">
        <v-card class="mx-auto mt-3">
          <v-card-text>
            <side-bar />
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import SideBar from "./SideBar";
export default {
  components: { SideBar },
  name: "DiceGame",
  data: () => ({}),
};
</script>
