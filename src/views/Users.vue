<template>
  <div>
    <div class="container-fluid pt-3 pb-5">
      <h2>User Table</h2>

      <b-row class="mb-3">
        <b-col>
          <b-form-group label="Filter:" label-for="search-filter" label-align="right" label-cols="4">
            <b-input-group>
              <b-form-input id="search-filter" v-model="filter" type="search" placeholder="Search..."></b-form-input>
              <b-button @click="filter=''">Clear</b-button>
            </b-input-group>
          </b-form-group>
        </b-col>
      </b-row>

      <b-row>
        <b-col>
          <b-table responsive head-variant="dark" bordered striped hover :items="users" :fields="fields" :filter="filter" :per-page="perPage" :current-page="currentPage" @filtered="getFilteredResults" caption-top>

            <template v-slot:cell(actions)="data">
              <b-icon icon="trash-fill" class="action-icons" @click="confirmDelete(data.item.id)"></b-icon>
              <b-icon icon="pencil-fill" class="action-icons" @click="$router.push({ name: 'EditUser', params: { user_id: data.item.id } })"></b-icon>
            </template>

            <template v-if="filter" #table-caption>{{ filteredResults }} result(s) found.</template>

          </b-table>
        </b-col>
      </b-row>
      
      <!-- Table Footer -->
      <b-row align-h="between">
        <b-col cols="4">
          <b-pagination pills size="sm" align="left" v-model="currentPage" :total-rows="rows" :per-page="perPage"></b-pagination>
        </b-col>
        <!-- <b-col cols="4" class="text-right mr-2">
          <b-button variant="primary" @click="$router.push({ name: 'AddUser'})">Add User</b-button>
        </b-col> -->
      </b-row>
    </div>

  </div>
  


</template>

<script>
export default {
  name: 'Users',
  data() {
    return {
      users: [],
      fields: [
        { key: 'id', label: 'ID', class: 'centered-cell'},
        'name', 
        'email',
        { key: 'userType', label: 'UT'}, 
        'paid',
        // { key: 'manual_access', label: 'MA'},
        'accessUntil',
        { key: 'actions', label: 'Actions', class: 'centered-cell'}],
      filter: '',
      perPage: 8,
      currentPage: 1,
      filteredResults: 0,
      confirmValue: ''
    }
  },
  computed: {
    rows() {
      return this.users.length
    }
  },
  methods: {
    deleteUser(id) {
      this.users = this.users.filter((user) => {
        return user.id !== id
      })
    },
    getFilteredResults(arr, num) {
      this.filteredResults = num
    },
    confirmDelete(id) {
      this.confirmValue = ''
      this.$bvModal.msgBoxConfirm('¿Estás segura?', {
        size: 'sm',
        okVariant: 'danger',
        okTitle: 'Sí',
        cancelTitle: 'Cancelar',
        centered: true
      })
        .then(value => {
          this.deleteUser(id)
        })
        .catch(err => {
          console.log('An error ocurred')
        })
    }
  },
  mounted() {
    fetch('http://localhost:3000/users')
      .then(res => res.json())
      .then(data => this.users = data)
      .catch(err => console.log(err.message))
  },
}
</script>

<style>
.action-icons {
  margin: 2px 4px;
  cursor: pointer;
  color: #bbb;
}
.action-icons:hover {
  color: #777;
}
.centered-cell {
  text-align: center;
}
</style>