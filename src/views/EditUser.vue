<template>
  <div class="container pt-3">
    <button @click="$router.push({ name: 'Users' })">Go Back</button>
    <h2>Edit User</h2>

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
            :disabled="disableInputs"
          ></b-form-input>
        </b-form-group>

        <!-- Name -->
        <b-form-group id="input-group-2" label="Nombre:" label-for="input-2">
          <b-form-input
            id="input-2"
            v-model="form.name"
            placeholder="Ingrese el nombre completo..."
            required
            :disabled="disableInputs"
          ></b-form-input>
        </b-form-group>

        <!-- Phone Number -->
        <b-form-group id="input-group-tel" label="Teléfono:" label-for="input-tel">
          <b-form-input
            id="input-tel"
            v-model="form.phone"
            placeholder="Ingrese el teléfono..."
            type="tel"
            :disabled="disableInputs"
            :state="telState"
            required
          ></b-form-input>
          <b-form-invalid-feedback id="input-group-tel">
            El número debe ser de al menos 10 dígitos
          </b-form-invalid-feedback>
        </b-form-group>

        <!-- User Type -->
        <b-form-group id="input-group-3" label="Tipo de usuaria:" label-for="input-3">
          <b-form-select
            id="input-3"
            v-model="form.user_type"
            :options="user_types"
            required
          ></b-form-select>
        </b-form-group>

        <!-- Login Type -->
        <b-form-group id="input-group-4" label="Login:" label-for="input-4">
          <b-form-input
            id="input-4"
            v-model="form.login_type"
            required
            disabled
          ></b-form-input>
        </b-form-group>

        <!-- Paid -->
        <b-row align-v="center">
          <b-col>
            <b-form-group id="input-radio-group" label="Pagado:" label-for="radio-group" v-slot="{ ariaDescribedby }">
              <b-form-radio-group
                id="radio-group"
                v-model="form.paid"
                :aria-describedby="ariaDescribedby"
                :options="paid_options"
              >
              </b-form-radio-group>
              <!-- <b-form-text v-if="!form.paid">Para dar acceso manual, selecciona "Sí"</b-form-text> -->
            </b-form-group>
            
          </b-col>

          <b-col v-if="!form.paid">
            <b-button v-if="!enableManualAccess" size="sm" variant="info" @click="enableManualAccess=!enableManualAccess">Habilitar Acceso Manual</b-button>
            <b-button v-if="enableManualAccess" size="sm" variant="info" @click="enableManualAccess=!enableManualAccess">Deshabilitar Acceso Manual</b-button>            
          </b-col>
        </b-row>
        <!-- Manual Access Control -->
        <div class="mt-2 mb-2">
          <label for="access_until">Acceso hasta:</label>
          <b-form-datepicker id="access_until" v-model="form.access_until" :disabled="manualAccess"></b-form-datepicker>
        </div>

        <!-- Submit -->
        <b-button type="submit" variant="primary">Aceptar</b-button>
      </b-form>
    </div>

    <!-- Test Form -->
    <!-- <b-card class="mt-3" header="Form Data Result">
      <pre class="m-0">{{ form }}</pre>
    </b-card> -->
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
        login_type: '',
        access_until: '',
        phone: '',
      },
      user_types: ['user', 'coach', 'admin'],
      paid_options: [
        { text: "Sí", value: true},
        { text: "No", value: false}
      ],
      disableInputs: false,
      enableManualAccess: false
    }
  },
  methods: {
    onSubmit() {

    }
  },
  computed: {
    telState() {
      if (this.form.phone.length > 0) {
        return this.form.phone.length > 9 ? true : false
      }
      else {
        return null;
      }
    },
    manualAccess() {
      return !(this.form.paid || this.enableManualAccess)
    }
  },
  mounted() {
    let uri = "http://localhost:3000/users/" + this.$route.params.user_id
    fetch(uri)
      .then(res => res.json())
      .then(data => {
        this.form.name = data.name
        this.form.email = data.email
        this.form.paid = data.paid
        this.form.user_type = data.user_type
        this.form.phone = data.phone
        this.form.access_until = data.access_until
        this.form.login_type = data.login_type
        if (this.form.login_type !== "email") {
          this.disableInputs = true
        }
      })
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