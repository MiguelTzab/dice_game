<template>
  <v-dialog v-model="dialog" persistent max-width="390">
    <v-card>
      <v-card-title class="headline">
        Nuevo Dado
      </v-card-title>
      <v-card-text>
        <v-form v-model="valid" ref="form" @submit.prevent="onSave">
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field
                  v-model="sides"
                  :rules="sidesRules"
                  label="Caras"
                  ref="sides"
                  required
                ></v-text-field>
              </v-col>
            </v-row>
          </v-container>
        </v-form>
      </v-card-text>
      <v-card-actions>
        <v-spacer></v-spacer>
        <v-btn color="red darken-1" text @click="onCancel">
          Cancelar
        </v-btn>
        <v-btn color="green darken-1" text @click="onSave">
          Guardar
        </v-btn>
      </v-card-actions>
    </v-card>
  </v-dialog>
</template>

<script>
export default {
  name: "AddDice",
  data: () => ({
    dialog: true,
    valid: false,
    sides: "",
    sidesRules: [
      (v) => !!v || "Campo requerido",
      (v) => v > 1 || "El número de caras no puede ser menor a 2",
      (v) => v <= 100 || "El número no puede ser mayor a 100",
    ],
  }),
  methods: {
    onCancel() {
      this.$refs.form.reset();
      this.$emit("cancel");
    },
    onSave() {
      if (this.valid) {
        this.$emit("save", this.sides);
      } else {
        this.$refs.form.validate();
      }
    },
  },
  mounted() {
    const inputs = this.$refs.sides.$el.getElementsByTagName("input");
    if (inputs && inputs.length > 0) {
      setTimeout(function() {
        inputs[0].focus();
      }, 50);
    }
  },
};
</script>

<style></style>
