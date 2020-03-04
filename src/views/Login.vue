<template>
  <div class="login">
    <div class="form">
      <form action="#" method="post">
       <span v-if="error != ''" class="error"> {{error}}</span><br><br>

        <label for="username">Nombre:</label>
        <br />
        <input type="text" v-model="username" />
        <br />
        <br />
        <label for="password">Contraseña:</label>
        <br />
        <input type="password" v-model="password" />
        <br />
        <br />
        <input type="button" value="Entrar" @click="login()" />
      </form>
    </div>
  </div>
</template>

<script>
// @ is an alias to /src
//import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: "Login",
  data() {
    return {
      username: "usuario1",
      password: "password1",
      error:"",        
    }
  },
  methods: {
    login() {
     console.log(this.username);
      var storage = window.localStorage;
      var users = JSON.parse(storage.getItem("users"));
      var loginOK = false;
      this.error ="";

      users.forEach(user => {
        if (this.username == user.name) {
          if (this.password == user.password) {
            loginOK = true;
            //si usuario y contraseña coinciden guardo ese usuario
           storage.setItem("userLog", JSON.stringify(user.name));
          }
        }
      });

        if (loginOK) {
          console.log("Usuario logueado correctamente");
            
           


          this.error="";
          this.$router.push({name:'Main'});
        } else {
          console.log("Usuario o contraseña no válidos");
          this.error = "Usuario o contraseña no válidos";
        }
      
    }
  }
};
</script>

<style scoped>
.form {
  background-color: beige;
}

.error{
  color: red;
}
</style>