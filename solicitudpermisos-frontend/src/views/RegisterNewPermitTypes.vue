<template>
  <div>
    <b-form @submit="onSubmit" @reset="onReset" v-if="show">
      <b-form-group id="input-group-1" label="Descripción" label-for="input-1">
        <b-form-input
          id="input-1"
          v-model="form.descripcion"
          type="text"
          required
          placeholder="Descripción"
        ></b-form-input>
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
  name: "RegisterNewPermitTypes",
  data() {
    return {
      form: {
        descripcion: "",
      },
      show: true,
    };
  },
  methods: {
    onSubmit() {
      axios
        .post("https://localhost:5001/api/TypePermission/RegisterPermitTypes", this.form)
        .then((response) => {
          console.log(response);
        })
        .catch((error) => {
          console.log(error);
        });
      alert(JSON.stringify(this.form));
    },
    onReset(evt) {
      evt.preventDefault();
      // Reset our form values
      this.form.Descripcion = "";
      // Trick to reset/clear native browser form validation state
      this.show = false;
      this.$nextTick(() => {
        this.show = true;
      });
    },
  },
};
</script>

<style>
</style>