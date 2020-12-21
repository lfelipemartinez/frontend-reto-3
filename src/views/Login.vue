<template>
  <div class="container login-container">
    <div class="row">
      <div class="col-md-6 login-form-1">
        <h2 class="text-primary">Login</h2>
        <form @submit.prevent="loginUser">
          <div class="form-group">
            <input
              type="text"
              class="form-control"
              placeholder="Email"
              v-model="login.email"
            />
          </div>
          <div class="form-group">
            <input
              type="password"
              class="form-control"
              placeholder="Contraseña"
              v-model="login.password"
            />
          </div>
          <div class="form-group">
            <input type="submit" class="btnSubmit" value="Iniciar de sesión" />
          </div>
          <div class="form-group">
            <a href="#" class="ForgetPwd">Olvidaste la contraseña?</a>
          </div>
        </form>
      </div>
    </div>
  </div>
</template>
<script>
import swal from "sweetalert";
export default {
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
    };
  },
  methods: {
    async loginUser() {
      try {
        let response = await this.$http.post("/api/auth/signin", this.login);
        console.log(response.data);
        let token = response.data.accessToken;
        localStorage.setItem("jwt", token);
        if (token) {
          swal("Exitoso", "login exitoso", "success");
          this.$router.push("/home");
        }
      } catch (err) {
        swal("Error", "datos incorrectos", "error");
        console.log(err.response);
      }
    },
  },
};
</script>

<style>

.login-container {
  margin-top: 5%;
  margin-bottom: 5%;
}
.login-form-1 {
  padding: 5%;
  box-shadow: 0 5px 8px 0 rgba(0, 0, 0, 0.2), 0 9px 26px 0 rgba(0, 0, 0, 0.19);
}
.login-form-1 h2 {
  text-align: center;
  color: #333;
}
.login-container form {
  padding: 10%;
}
.btnSubmit {
  width: 50%;
  border-radius: 1rem;
  padding: 1.5%;
  border: none;
  cursor: pointer;
}
.login-form-1 .btnSubmit {
  font-weight: 600;
  color: #fff;
  background-color: #0062cc;
}
.login-form-1 .ForgetPwd{
    color: #0062cc;
    font-weight: 600;
    text-decoration: none;
}
</style>