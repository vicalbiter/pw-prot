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
            required
          ></b-form-input>
          <!-- <b-form-invalid-feedback id="input-group-tel">
            El número debe ser de al menos 10 dígitos
          </b-form-invalid-feedback> -->
        </b-form-group>

        <!-- User Type -->
        <b-form-group id="input-group-3" label="Tipo de usuaria:" label-for="input-3">
          <b-form-select
            id="input-3"
            v-model="form.userType"
            :options="userTypes"
            required
          ></b-form-select>
        </b-form-group>

        <!-- Login Type -->
        <b-form-group id="input-group-4" label="Login:" label-for="input-4">
          <b-form-input
            id="input-4"
            v-model="form.loginType"
            required
            disabled
          ></b-form-input>
        </b-form-group>


        <!-- Paid Info -->
        <div v-if="form.userType === 'user'">
           <!-- Paid Radio Buttons-->
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
              <b-button v-if="!enableManualAccess" size="sm" variant="warning" @click="enableManualAccess=!enableManualAccess">Habilitar Acceso Manual</b-button>
              <b-button v-if="enableManualAccess" size="sm" variant="warning" @click="enableManualAccess=!enableManualAccess">Deshabilitar Acceso Manual</b-button>            
            </b-col>
          </b-row>
          <!-- Manual Access Control -->
          <div class="mt-2 mb-4">
            <label for="accessUntil">Acceso hasta:</label>
            <b-form-datepicker id="accessUntil" v-model="form.accessUntil" :disabled="manualAccess"></b-form-datepicker>
          </div>
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
        userType: '',
        loginType: '',
        accessUntil: '',
        phone: '',
      },
      userTypes: ['user', 'coach', 'admin'],
      paid_options: [
        { text: "Sí", value: true},
        { text: "No", value: false}
      ],
      uri: '',
      disableInputs: false,
      enableManualAccess: false
    }
  },
  methods: {
    onSubmit() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { 'Content-Type': 'application/json' },
        body: JSON.stringify({ 
          name: this.form.name, 
          email: this.form.email,
          paid: this.form.paid,
          userType: this.form.userType,
          phone: this.form.phone,
          accessUntil: this.form.accessUntil,
          loginType: this.form.loginType 
        })
      }).then(() => { 
        this.$router.push({ name: 'Users'})
      }).catch((err) => console.log(err.message))
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
    this.uri = "http://localhost:3000/users/" + this.$route.params.user_id
    fetch(this.uri)
      .then(res => res.json())
      .then(data => {
        this.form.name = data.name
        this.form.email = data.email
        this.form.paid = data.paid
        this.form.userType = data.userType
        this.form.phone = data.phone
        this.form.accessUntil = data.accessUntil
        this.form.loginType = data.loginType
        if (this.form.loginType !== "email") {
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