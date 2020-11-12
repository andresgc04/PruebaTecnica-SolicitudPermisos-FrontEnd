<template>
  <div class="home">
    <div id="buttonPositions">
      <b-button
        id="buttonRegisterNewPermit"
        variant="outline-primary"
        @click="registerNewPermitView()"
        >Register New Permit Types</b-button
      >
      <b-button variant="outline-primary" @click="registerNewPermitView()"
        >Permit Types</b-button
      >
    </div>
    <b-table striped hover :items="data"></b-table>
  </div>
</template>

<script>
import axios from "axios";
export default {
  name: "HomePermitTypes",
  data() {
    return {
      fields: [
        { key: "nombreEmpleado", label: "Nombre del Empleado" },
        { key: "apellidosEmpleado", label: "Apellidos del Empleado" },
        { key: "tipoPermiso", label: "Tipo del Permiso" },
        { key: "fechaPermiso", label: "Fecha del Permiso" },
      ],
      data: [],
    };
  },
  methods: {
    getItem() {
      axios
        .get("https://localhost:5001/api/TypePermission/ListOfTypesOfPermits")
        .then((response) => {
          this.data = response.data.data;
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
    },
    registerNewPermitView() {
      this.$router.push({
        name: "RegisterNewPermit",
      });
    },
  },
  created() {
    this.getItem();
  },
};
</script>

<style>
</style>