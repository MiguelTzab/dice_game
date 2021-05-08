<template>
  <v-dialog v-model="dialog" persistent max-width="390">
    <v-card>
      <v-card-title class="headline">
        Nuevo Jugador
      </v-card-title>
      <v-card-text>
        <v-form v-model="valid" ref="form" @submit.prevent="onSave">
          <v-container>
            <v-row>
              <v-col cols="12">
                <v-text-field
                  v-model="name"
                  :rules="nameRules"
                  :counter="10"
                  label="Nombre"
                  ref="name"
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
  name: "AddPlayer",
  data: () => ({
    dialog: true,
    valid: false,
    name: "",
    nameRules: [
      (v) => !!v || "Campo requerido",
      (v) =>
        v.length <= 12 || "El nombre debe ser menor o igual de 12 caracteres",
    ],
  }),
  methods: {
    onCancel() {
      this.$refs.form.reset();
      this.$emit("cancel");
    },
    onSave() {
      if (this.valid) {
        this.$emit("save", this.name);
      } else {
        this.$refs.form.validate();
      }
    },
  },
  mounted() {
    const inputs = this.$refs.name.$el.getElementsByTagName("input");
    if (inputs && inputs.length > 0) {
      setTimeout(function() {
        inputs[0].focus();
      }, 50);
    }
  },
};
</script>

<style></style>
