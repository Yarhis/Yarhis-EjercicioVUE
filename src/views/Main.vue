<template>
  <div class="main">
   <!-------------------------------------->
    <p>Hola, {{userOnSession}}</p>
    
    <label for="descripcion">Escriba la nueva tarea:</label>
    <input name="descripcion" v-model="newTaskDescription" placeholder="Describa la tarea que desee">
<button v-on:click="createTask" > Guardar</button>

<FormTask v-if="taskToChange" v-bind:taskToModify="taskToChange" v-on:updateDataTask="modifyTask($event)"></FormTask>
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
<Task v-for="(task, key) in tasks" v-bind:key="key" 
v-bind:task="task" 
v-on:deleteTask="removeTask(key)" 
v-on:showForm="showForm($event)"
></Task>
</tbody>
</table>

<!-------------------------------------->
  </div>
</template>

<script>
 var storage = window.localStorage;     

import Task from '@/components/Task.vue'
import FormTask from '@/components/FormTask.vue'


export default {
  name: "Main",
  components:{Task,FormTask},
  data() {
    return {
      tasks: "",
      newTaskDescription: "", 
      oldTaskDescription:"",    
      userOnSession:this.$route.params.loguedUser,
      taskToChange: ""
          
    }
},
 mounted() {      
   
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
  showForm:function(v){
    this.taskToChange= v;
    this.oldTaskDescription = v.desc;
  },
    //borrar funcion si funciona en task.vue
    modifyTask: function (v2) {
    //  console.log(key,task.__ob__.value.desc);
     console.log(v2);
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