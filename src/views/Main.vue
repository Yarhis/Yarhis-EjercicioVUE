<template>
  <div class="main">
   <!-------------------------------------->
    <p>Hola, {{userOnSession}}</p>

     <p>Crea una tarea:</p>
    
    <label for="descripcion">Descripción de la tarea:</label>
    <input name="descripcion" v-model="taskForm.desc" placeholder="Describa la tarea que desee">
<button v-on:click="guardaTask" > Guardar</button>

<!-- <label for="createUser">Usuarios disponibles</label>
<select name="userChoices" id="userChoices"  >
<option v-for="user in users" :key="user.name" >
   {{user.name}}
</option>
</select>
<br>

<label for="states" >Estados</label>
<select name="states" id="states" v-model="taskForm.state">
  <option v-for="state in statesTasks" :key="state" >
   {{state}}
</option>
</select> -->




    <p>Lista de tareas</p>

<Task v-for="(task, key) in tasks" v-bind:key="key" v-bind:task="task"></Task>


<!-------------------------------------->
  </div>
</template>

<script>
import Task from '@/components/Task.vue'

export default {
  name: "Main",
  components:{Task},
  data() {
    return {
      tasks: "",
      taskForm:{
        desc: "",
        create_date:new Date(),
        create_user: this.$route.params.loguedUser,
        state: "Iniciada", 
        close_user:null
      },
      users:null,
      userOnSession:this.$route.params.loguedUser,
      statesTasks:null
    }
},
 mounted() {
       var storage = window.localStorage;     
    this.users = JSON.parse(storage.getItem("users"));
    this.statesTasks = JSON.parse(storage.getItem("estados"));
     this.tasks = JSON.parse(storage.getItem("tasks"));

  },
  methods:{
  guardaTask:function(){
     var storage = window.localStorage; 
      var tasksList= this.tasks;
tasksList.push(this.taskForm);

     storage.setItem("tasks", JSON.stringify(tasksList));
  }
  }
}
</script>

<style scoped>
.form {
  background-color: beige;
}
</style>