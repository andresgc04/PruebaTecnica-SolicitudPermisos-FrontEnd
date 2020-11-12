<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group
        id="input-group-1"
        label="Nombre del Empleado:"
        label-for="input-1"
      >
        <b-form-input
          id="input-1"
          v-model="form.email"
          type="email"
          required
          placeholder="Ingrese el nombre del empleado"
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-2"
        label="Apellidos del Empleado"
        label-for="input-2"
      >
        <b-form-input
          id="input-2"
          v-model="form.name"
          required
          placeholder="Ingrese los apellidos del empleado"
        ></b-form-input>
      </b-form-group>

      <b-form-group
        id="input-group-3"
        label="Tipo de Permiso"
        label-for="input-3"
      >
        <b-form-select
          id="input-3"
          v-model="form.dataTypeOfPermits"
          :options="dataTypeOfPermits"
          required
        ></b-form-select>
      </b-form-group>

      <b-form-group>
        <label for="example-datepicker">Fecha de Permiso</label>
        <b-form-datepicker
          id="example-datepicker"
          v-model="form.fechaNacimiento"
          class="mb-2"
        ></b-form-datepicker>
        <p>Value: '{{ form.fechaNacimiento }}'</p>
      </b-form-group>

      <b-button type="submit" variant="primary">Submit</b-button>
      <b-button type="reset" variant="danger">Reset</b-button>
    </b-form>
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "RegisterNewPermit",
  data() {
    return {
      form: {
        email: "",
        name: "",
        food: null,
        fechaNacimiento: "",
      },
      foods: [
        { text: "Seleccione un Permiso", value: null },
        "Carrots",
        "Beans",
        "Tomatoes",
        "Corn",
      ],
      dataTypeOfPermits: [],
      show: true,
    };
  },
  methods: {
    onSubmit(evt) {
      evt.preventDefault();
      alert(JSON.stringify(this.form));
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.email = "";
      this.form.name = "";
      this.form.food = null;
      this.form.fechaNacimiento = "";
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
    getTypesOfPermits() {
      axios
        .get("https://localhost:5001/api/TypePermission/ListOfTypesOfPermits")
        .then((response) => {
          this.dataTypeOfPermits = response.data.data;
          console.log(response.data.data);
        })
        .catch((error) => {
          console.log(error);
        });
    },
  },
  created() {
    this.getTypesOfPermits();
  },
};
</script>

<style>
</style>