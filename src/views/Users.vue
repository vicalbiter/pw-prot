<template>
  <div>
    
    <div class="container-fluid pt-3 pb-5">
      <h3>User Table</h3>

      <b-row align-h="between" class="mb-1">
        <!-- Results per Page -->
        <b-col cols="4">
          <b-form-group label="Per page:" label-for="per-page-select" label-cols="5" label-align="left" label-size="sm">
            <b-form-select id="per-page-select" size="sm" v-model="perPage" :options="pageOptions"></b-form-select>
          </b-form-group>
        </b-col>
        <!-- Filter Search -->
        <b-col cols="6">
          <b-form-group label="Filter:" label-for="search-filter" label-align="right" label-cols="2" label-size="sm">
            <b-input-group>
              <b-form-input id="search-filter" size="sm" v-model="filter" type="search" placeholder="Search..."></b-form-input>
              <b-button class="ml-1" size="sm" @click="filter=''">Clear</b-button>
            </b-input-group>
          </b-form-group>
        </b-col>
      </b-row>

      <b-row>
        <b-col>
          <b-table responsive outlined hover :items="users" :fields="fields" :filter="filter" :per-page="perPage" :current-page="currentPage" @filtered="getFilteredResults" caption-top class="user-table">

            <template v-slot:cell(actions)="data">
              <b-icon icon="trash-fill" class="action-icons icon-delete" @click="confirmDelete(data.item.id)"></b-icon>
              <b-icon icon="pencil-fill" class="action-icons icon-edit" @click="$router.push({ name: 'EditUser', params: { user_id: data.item.id } })"></b-icon>
            </template>

            <!-- <template v-if="filter" #table-caption>{{ filteredResults }} result(s) found.</template> -->

          </b-table>
        </b-col>
      </b-row>
      
      <!-- Table Footer -->
      <b-row align-h="between">
        <b-col cols="4">
          <div v-if="!filter">
            <b-pagination pills size="sm" align="left" v-model="currentPage" :total-rows="rows" :per-page="perPage"></b-pagination>
          </div>
          <div v-else>
            <b-pagination pills size="sm" align="left" v-model="currentPage" :total-rows="filteredRows" :per-page="perPage"></b-pagination>
          </div>
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
      filteredUsers: [],
      fields: [
        { key: 'id', label: 'ID', class: 'centered-cell'},
        { key: 'name', label: 'Nombre'}, 
        'email',
        { key: 'userType', label: 'Tipo'}, 
        { key: 'paid', label: 'Pagado'},
        // { key: 'manual_access', label: 'MA'},
        { key: 'accessUntil', label: 'Exp. Acceso'},
        { key: 'actions', label: 'Acciones', class: 'centered-cell'}],
      filter: '',
      perPage: 5,
      currentPage: 1,
      currentFilteredPage: 1,
      filteredResults: 0,
      pageOptions: [5, 10, 20],
      confirmValue: ''
    }
  },
  computed: {
    rows() {
      return this.users.length
    },
    filteredRows() {
      return this.filteredUsers.length
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
      this.filteredUsers = arr
      this.currentPage = 1
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
  padding: 3px;
  border: solid 1px #bbb;
  border-radius: 5px;
  font-size: 1.5em;
}

.action-icons:hover {
  color: rgb(119, 119, 119);
}

/* .icon-delete {
  border: solid 1px #f97d7d;
  color: #f97d7d;
}

.icon-delete:hover {
  border: solid 1px #f73434;
  color: #f73434;
}

.icon-edit {
  border: solid 1px #78ecff;
  color: #78ecff;
}

.icon-edit:hover {
  border: solid 1px #0eddff;
  color: #0eddff;
} */


.centered-cell {
  text-align: center;
}

.user-table {
  background-color: white;
}
</style>