<template>
  <div class="d-flex">
    <!-- Side Bar -->
    <div id="side-drawer" class="side-nav d-flex flex-column" :class="{ showdrawer: showDrawer }">
      <div class="logo">PinkWorkout</div>

      <div class="side-nav-menu">
        <b-list-group class="list-group-flush">
          <b-list-group-item active>Active</b-list-group-item>
          <b-list-group-item>Link</b-list-group-item>
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

    <!-- Main Content -->
    <div class="main-screen w-100">
      <!-- Top Navbar -->
      <div class="top-nav">
        <b-navbar toggleable="md" type="dark" variant="info">
          <b-navbar-brand href="#" @click="showDrawer = !showDrawer"><b-icon icon="list"></b-icon> NavBar</b-navbar-brand>

          <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

          <b-collapse id="nav-collapse" is-nav>
            <!-- Left aligned nav items -->
            <b-navbar-nav>
              <b-nav-item href="#">Link</b-nav-item>
            </b-navbar-nav>

            <!-- Right aligned nav items -->
            <b-navbar-nav class="ml-auto">
              <b-nav-form>
                <b-form-input size="sm" class="mr-sm-2" placeholder="Search"></b-form-input>
                <b-button size="sm" class="my-2 my-sm-0" type="submit">Search</b-button>
              </b-nav-form>

              <b-nav-item-dropdown right>
                <!-- Using 'button-content' slot -->
                <template #button-content>
                  <em>User</em>
                </template>
                <b-dropdown-item href="#">Profile</b-dropdown-item>
                <b-dropdown-item href="#">Sign Out</b-dropdown-item>
              </b-nav-item-dropdown>
            </b-navbar-nav>
          </b-collapse>
        </b-navbar>
      </div>

      <div class="content">

      </div>
      <!-- <router-view></router-view> -->

    </div>

  </div>
</template>

<script>
export default {
  data() {
    return {
      showDrawer: false
    }
  }
}
</script>

<style>
.side-nav {
  min-height: 100vh;
  width: 12rem;
  margin-left: -12rem;
  transition: margin .25s ease-in-out;
  background-color: #fff;
}

.showdrawer {
  margin-left: 0;
}

.side-nav .logo {
  padding: .875rem 1.25rem;
  font-size: 1.2rem;
}
.top-nav {

}

body {
  background-color: #fff;
}

</style>