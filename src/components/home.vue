<template>
 <div>
   <nav
    class="navbar navbar-expand-sm navbar-dark font-weight-bold justify-content-start bg-dark"
  >
    <!-- nav logo -->
    <a class="navbar-brand" href="#">
      <img src="../assets/logo.png"  class="img" alt="Logo" height="50px" />
    </a>
    <!-- boton collapse-->
    <button
      class="navbar-toggler"
      type="button"
      data-toggle="collapse"
      data-target="#collapsibleNavbar"
    >
      <span class="navbar-toggler-icon"></span>
    </button>
    <!--fin del boton collapse-->
    <!-- fin del logo -->
    <!--navbar list-->
    <div
      class="collapse navbar-collapse justify-content-end"
      id="collapsibleNavbar"
    >
      <ul class="navbar-nav">
        <li class="nav-item"><a class="nav-link active" href="#">Home</a></li>
        <li class="nav-item">
          <a class="nav-link" @click="logUserOut">Salir</a>
        </li>
      </ul>
    </div>
    <!-- fin del navbar list-->
  </nav>
 <section>
 <div class="container mt-5">
 <div class="row">
 <div class="col-md-12">
 <ul class="list-group">
 <li class="list-group-item">Name : {{ user.name }}</li>
 <li class="list-group-item">Email : {{ user.email }}</li>
 </ul>
 </div>
 </div>
 </div>
 </section>
 </div>
</template>
<script>
import VueJwtDecode from "vue-jwt-decode";
export default {
 data() {
 return {
 user: {}
 };
 },
 methods: {
 getUserDetails() {
 let token = localStorage.getItem("jwt");
 let decoded = VueJwtDecode.decode(token);
 console.log('hola decode',decoded);
 this.user = decoded;
 },
 logUserOut() {
 localStorage.removeItem("jwt");
 this.$router.push("/");
 }
 },
 created() {
 this.getUserDetails();
 }
};
</script>
<style scoped></style>