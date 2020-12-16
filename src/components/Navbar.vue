<template>

  <div>
    <!-- Top Navbar Menu -->
    <div class="top-nav">
      <b-navbar type="dark" variant="info">
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
            <b-list-group-item :to="{ name: 'Home' }">Home</b-list-group-item>
            <b-list-group-item :to="{ name: 'About' }">About</b-list-group-item>
            <b-list-group-item>Another Link</b-list-group-item>
            <b-list-group-item disabled>Disabled</b-list-group-item>
          </b-list-group>
        </div>

        <div class="side-nav-footer mt-auto">
          <b-list-group class="list-group-flush">
            <b-list-group-item>Link</b-list-group-item>
            <b-list-group-item>Another Link</b-list-group-item>
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
  min-height: calc(100vh - 56px);
  width: 14rem;
  margin-left: -14rem;
  transition: margin .25s ease-in-out;
  background-color: #fff;
}

.side-nav .logo {
  padding: .875rem 1.25rem;
  font-size: 1.2rem;
}

#side-drawer a.router-link-exact-active {
  background-color:rgba(27,31,35,.05)
}

.showdrawer {
  margin-left: 0;
}

/* Top Navbar */
.top-nav {

}

/* Others */

</style>