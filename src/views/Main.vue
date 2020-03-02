<template>
  <div class="main">
   <!-------------------------------------->
    <p>Hola, {{userOnSession}}</p>
    
    <label for="descripcion">Escriba la nueva tarea:</label>
    <input name="descripcion" v-model="newTaskDescription" placeholder="Describa la tarea que desee">
<button v-on:click="createTask" > Guardar</button>

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
<table>
<thead>
   <tr>
      <th>Descripción</th>
      <th>Fecha de creación</th>
      <th>Usuario que crea la tarea</th>
      <th>estado</th>
      <th>usuario que cierra la tarea</th>
      <th>Modificar</th>
      <th>Eliminar</th>      
    </tr>
</thead>
<tbody>
<Task v-for="(task, key) in tasks" v-bind:key="key" v-bind:task="task" v-on:deleteTask="removeTask(key)"></Task>
</tbody>
</table>

<!-------------------------------------->
  </div>
</template>

<script>
 var storage = window.localStorage;     

import Task from '@/components/Task.vue'

export default {
  name: "Main",
  components:{Task},
  data() {
    return {
      tasks: "",
      newTaskDescription: "",     
      users:null,
      userOnSession:this.$route.params.loguedUser,
      statesTasks:null
    }
},
 mounted() {
      
    this.users = JSON.parse(storage.getItem("users"));
    this.statesTasks = JSON.parse(storage.getItem("estados"));
    this.tasks = JSON.parse(storage.getItem("tasks"));

  },
  methods:{
  createTask:function(){
    
    
     var newTask ={
        desc: this.newTaskDescription,
        create_date:new Date(),
        create_user: this.$route.params.loguedUser,
        state: "Iniciada", 
        close_user:null
      }
      this.newTaskDescription = "";
     this.tasks.push(newTask);
    
     
  },
  removeTask: function (key) {
     this.tasks.splice(key,1);
     
    },
    ModifyTask: function (key,task) {
     console.log(key,task.__ob__.value.desc);
     
    },
  },
  watch:{    
     handler:function(tasks){
      storage.setItem("tasks", JSON.stringify(tasks));
     
    }
  }
}
</script>

<style scoped>


</style>