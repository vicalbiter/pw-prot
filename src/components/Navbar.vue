<template>

  <div>
    <!-- Top Navbar Menu -->
    <div class="top-nav">
      <b-navbar type="dark" variant="primary">
        <b-navbar-brand href="#" @click="showDrawer = !showDrawer"><b-icon icon="list"></b-icon> Pink Workout</b-navbar-brand>

        <!-- Left aligned nav items -->
        <b-navbar-nav>
          <b-nav-item href="#">Link</b-nav-item>
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">

          <b-nav-item-dropdown text="Hello, User!" right>
            <b-dropdown-item href="#">Profile</b-dropdown-item>
            <b-dropdown-item href="#">Sign Out</b-dropdown-item>
          </b-nav-item-dropdown>
        </b-navbar-nav>

      </b-navbar>
    </div>

    <!-- Main Content -->
    <div class="d-flex">

      <!-- Side Navbar Menu -->
      <div id="side-drawer" class="side-nav d-flex flex-column" :class="{ showdrawer: showDrawer }">

        <div class="side-nav-menu">
          <b-list-group flush>
            <b-list-group-item :to="{ name: 'Home' }">
              <b-icon icon="house-door-fill"></b-icon>
              <span class="ml-2">Principal</span>
              </b-list-group-item>
            <b-list-group-item :to="{ name: 'Users' }">
              <b-icon icon="person-fill"></b-icon>
              <span class="ml-2">Lista de Usuarias</span>
              </b-list-group-item>
            <b-list-group-item>Another Link</b-list-group-item>
            <b-list-group-item disabled>Disabled</b-list-group-item>
          </b-list-group>
        </div>

        <div class="side-nav-footer mt-auto">
          <b-list-group class="list-group-flush">
            <b-list-group-item>Link</b-list-group-item>
            <b-list-group-item>
              <b-icon icon="box-arrow-in-left"></b-icon>
              Salir
            </b-list-group-item>
          </b-list-group>
        </div>
      </div>

      <!-- Content -->
      <div class="main-screen w-100">

        <router-view></router-view>

      </div>

    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      showDrawer: true
    }
  }
}
</script>

<style>
/* Body */
body {
  background-color: #f9f9f9;
}

/* Side Nav */
.side-nav {
  height: calc(100vh - 56px);
  width: 15rem;
  margin-left: -15rem;
  transition: margin .25s ease-in-out;
  background-color: #fff;
  border-width: 0 1px 0 0;
  border-style: solid;
  border-color: rgba(0,0,0,.05);
  font-size: 0.9rem;
}

.side-nav .logo {
  padding: .875rem 1.25rem;
  font-size: 1.2rem;
}

#side-drawer a.router-link-exact-active {
  background-color:rgba(27,31,35,.05);
  border-left: solid 5px var(--primary);
}

.showdrawer {
  margin-left: 0;
}

/* Top Navbar */
.top-nav {

}

/* Others */
.main-screen {
  height: calc(100vh - 56px);
  /* max-width: 100%; */
  overflow: auto;
}

</style>