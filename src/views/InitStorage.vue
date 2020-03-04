<template>
  <div class="initstorage">
    <h1>This is an InitStorage page</h1>
    <p>Usuarios:</p>
    <ol>
      <li v-for="(user, key) in users" v-bind:key="key">
        <span v-for="(value,key) in user" v-bind:key="key">{{key}}: {{ value }}; </span>
      </li>
    </ol>
    <p>Estados</p>
    <ol>
      <li v-for="(state, key) in states" v-bind:key="key">{{ state }}</li>
    </ol>
 <p>Tasks</p>
   <ol>
      <li v-for="(task, key) in tasks" v-bind:key="key">
        <span v-for="(value,key) in task" v-bind:key="key">{{key}}: {{ value }}; </span>
      </li>
    </ol>
  </div>
</template>

<script>
export default {
  name: "InitStorage",
  data() {
    return {
      users: "",
      states: "",
      tasks: ""
    };
  },
  mounted() {
    console.log("DEBUD: Montado!");
    var storage = window.localStorage;    
    this.initstorage();
   this.users = JSON.parse(storage.getItem("users"));
    this.states = JSON.parse(storage.getItem("estados"));
    this.tasks = JSON.parse(storage.getItem("tasks"));
   
  },
  methods: {
    initstorage() {
      console.log("DEBUG: En initstorage");
      var storage = window.localStorage;
      storage.clear();

      //Creación de estados
      var estados = new Array("Iniciada", "En curso", "Finalizada");

      //Creación de usuarios
      var users = new Array(
        { name: "usuario1", password: "password1" },
        { name: "usuario2", password: "password2" },
        { name: "usuario3", password: "password3" }
      );

      var tasks = new Array(
        {desc: "descripción de la tarea 1", create_date:new Date().toLocaleString(), create_user: "usuario1", state: "Iniciada", close_user:null},
        {desc: "descripción de la tarea 2", create_date:new Date().toLocaleString(), create_user: "usuario2", state: "curso", close_user:null},
       {desc: "descripción de la tarea 3", create_date:new Date().toLocaleString(), create_user: "usuario3", state: "Finalizada", close_user:null},
      );

      //Creación de tareas

      storage.setItem("users", JSON.stringify(users));
      storage.setItem("estados", JSON.stringify(estados));
      storage.setItem("tasks", JSON.stringify(tasks));
    }
  },
  //crear metodo para setear dinamicamente tareas, tanto crear como eliminar

};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>

