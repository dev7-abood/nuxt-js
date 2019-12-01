<template>
  <div>
    <b-navbar toggleable="lg" type="dark" variant="success">
      <b-navbar-brand to="/" class="font-weight-bold font-italic">Posts <span class="text-dark">Site</span></b-navbar-brand>

      <b-navbar-toggle target="nav-collapse"></b-navbar-toggle>

      <b-collapse id="nav-collapse" is-nav>
        <b-navbar-nav>
<!--          <b-nav-item to="/home">Home</b-nav-item>-->
          <b-nav-item :to="{name : 'topics'}" class="text-uppercase">Posts</b-nav-item>

          <b-nav-item v-if="authenticated" class="text-uppercase" :to="{name : 'create'}">create new topic</b-nav-item>

<!--          <b-nav-item href="#" disabled>SNIPER</b-nav-item>-->
        </b-navbar-nav>

        <!-- Right aligned nav items -->
        <b-navbar-nav class="ml-auto">

          <b-navbar-nav right v-if="!authenticated">
            <b-nav-item to="/login">Login</b-nav-item>
            <b-nav-item to="/register">Register</b-nav-item>
          </b-navbar-nav>

          <b-navbar-nav right v-else="authenticated">
            <ul class="navbar-nav ml-auto">
              <li class="nav-item">
                <a class="nav-link text-white">{{user.name}}</a>
              </li>
            </ul>
            <a href="#" @click.passive="logout" class="nav-link">Logout</a>
          </b-navbar-nav>

<!--          <b-nav-item-dropdown text="Lang" right>-->
<!--            <b-dropdown-item href="#">EN</b-dropdown-item>-->
<!--            <b-dropdown-item href="#">ES</b-dropdown-item>-->
<!--            <b-dropdown-item href="#">RU</b-dropdown-item>-->
<!--            <b-dropdown-item href="#">FA</b-dropdown-item>-->
<!--          </b-nav-item-dropdown>-->

<!--          <b-nav-item-dropdown right>-->
<!--            &lt;!&ndash; Using 'button-content' slot &ndash;&gt;-->
<!--            <template v-slot:button-content>-->
<!--              <em>User</em>-->
<!--            </template>-->
<!--            <b-dropdown-item href="#">Profile</b-dropdown-item>-->
<!--            <b-dropdown-item href="#">Sign Out</b-dropdown-item>-->
<!--          </b-nav-item-dropdown>-->
        </b-navbar-nav>
      </b-collapse>
    </b-navbar>

  </div>
</template>

<script>
    export default {
        name : "Navbar",
        methods : {
            logout(){
                this.$auth.logout()
            }
        }

    }
</script>

<style scoped>

</style>
