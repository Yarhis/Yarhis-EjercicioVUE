<template>
  <div class="main">
   <!-------------------------------------->
    <p>Hola, {{userOnSession}}</p>
    
    <label for="descripcion">Escriba la nueva tarea:</label>
    <input name="descripcion" v-model="newTaskDescription" placeholder="Describa la tarea que desee">
<button v-on:click="createTask" > Guardar</button>

<FormTask v-if="formEnable" v-bind:taskToModify="taskToChange" v-on:updateDataTask="modifyTask($event)"></FormTask>

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
v-on:showForm="showForm(key,task)"
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
      userOnSession:"",
      taskToChange: {},
      formEnable:false,
      taskPosition:""
          
    }
},
 mounted() {   
   
    this.tasks = JSON.parse(storage.getItem("tasks"));
 this.userOnSession = JSON.parse(storage.getItem("userLog"));
  },
  methods:{
  createTask:function(){
    
    
     var newTask ={
        desc: this.newTaskDescription,
        create_date:new Date(),
        create_user: this.userOnSession,
        state: "Iniciada", 
        close_user:null
      }
      this.newTaskDescription = "";
     this.tasks.push(newTask);
     storage.setItem("tasks", JSON.stringify(this.tasks));
    
     
  },
  removeTask: function (key) {
     this.tasks.splice(key,1);
     
    },
  showForm:function(key,task){
    this.formEnable= true;
    this.taskToChange= task;
    this.taskPosition =key;

  },
    //borrar funcion si funciona en task.vue
    modifyTask: function (mt) {
      this.tasks[this.taskPosition] = mt;
      storage.setItem("tasks", JSON.stringify(this.tasks));

      // this.formEnable= false;
    },
  },
  // watch:{    
  //    handler:function(tasks){
  //     storage.setItem("tasks", JSON.stringify(tasks));
     
  //   }
  // }
}
</script>

<style scoped>


</style>