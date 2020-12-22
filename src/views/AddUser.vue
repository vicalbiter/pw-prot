<template>
  <div class="container pt-3">
    <button @click="$router.push({ name: 'Users' })">Go Back</button>
    <h2>Add User</h2>

    <div class="form-container">
      <b-form @submit.prevent="onSubmit">

        <!-- Email -->
        <b-form-group
          id="input-group-1"
          label="Email:"
          label-for="input-1"
        >
          <b-form-input
            id="input-1"
            v-model="form.email"
            type="email"
            placeholder="Ingrese el email..."
            required
          ></b-form-input>
        </b-form-group>

        <!-- Name -->
        <b-form-group id="input-group-2" label="Nombre:" label-for="input-2">
          <b-form-input
            id="input-2"
            v-model="form.name"
            placeholder="Ingrese el nombre completo..."
            required
          ></b-form-input>
        </b-form-group>

        <!-- User Type -->
        <b-form-group id="input-group-3" label="Tipo:" label-for="input-3">
          <b-form-select
            id="input-3"
            v-model="form.user_type"
            :options="user_types"
            required
          ></b-form-select>
        </b-form-group>

        <!-- Paid -->
        <b-form-group label="Pagado:" v-slot="{ ariaDescribedby }" description="Para dar acceso manual, selecciona 'Sí'">
          <b-form-radio-group
            id="radio-group-2"
            v-model="form.paid"
            :aria-describedby="ariaDescribedby"
          >
            <b-form-radio value="yes">Sí</b-form-radio>
            <b-form-radio value="no">No</b-form-radio>
          </b-form-radio-group>

          <!-- Manual Access Control -->
          <div v-if="form.paid === 'yes'">
            <label for="access_until">Access until:</label>
            <b-form-datepicker id="access_until" v-model="form.access_until"></b-form-datepicker>
          </div>
        </b-form-group>

        <!-- Submit -->
        <b-button type="submit" variant="primary">Submit</b-button>
      </b-form>
    </div>
    
    <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card>
  </div>  
</template>

<script>
export default {
  data() {
    return {
      form: {
        name: '',
        email: '',
        paid: 'no',
        user_type: '',
        manual_acces: '',
        login_type: '',
        access_until: '',
      },
      user_types: ['user', 'coach', 'admin']
    }
  },
  methods: {
    onSubmit() {

    }
  }
}
</script>

<style>
.form-container {
  margin: 20px;
  padding: 20px;
  border: 1px solid rgba(0, 0, 0, 0.3);
  border-radius: 5px;
}
</style>