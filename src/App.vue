<template>
  <div id="app">
    <div class="row">
      <div v-if="receeve_user" class="col-sm-12" @user-data-updated="userDataUpdated">
        <b-navbar toggleable="lg" type="dark" variant="info">
          <b-navbar-brand href="#"><router-link to="/dashboard"><span class="dashboard-menu">Dashboard</span></router-link></b-navbar-brand>
          <b-navbar-brand href="#"><router-link to="/accounts">Accounts</router-link></b-navbar-brand>
          <b-navbar-brand @click="logout" href="#">Logout</b-navbar-brand>
        </b-navbar>
      </div>
      <div class="col-sm-12">
        <router-view></router-view>
      </div>
    </div>
  </div>
</template>

<script>

export default {
  name: 'app',
  data() {
    return {
      receeve_user:""
    }
  },
  watch:{
      $route(to, from){
        console.log({to, from});
        this.receeve_user = localStorage.getItem('receeve_user');  
      }
  },
  mounted(){
    this.receeve_user = localStorage.getItem('receeve_user');
  },
  methods:{
    userDataUpdated: function () {
      console.log("userDataUpdated called");
      this.receeve_user = localStorage.getItem('receeve_user');
    },
    logout: function () {
      localStorage.removeItem('receeve_user');
      this.$router.push({ name: "Login"});
    }
  }
}
</script>
<style>
.navbar a{
  color: #343a40;
  text-decoration: none;
}
.dashboard-menu {
  padding-left:20px;
}
</style>