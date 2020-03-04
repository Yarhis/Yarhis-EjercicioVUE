<template>
  <form class="modal" >
    <div class="modal-content">
      <p>MODIFICAR TAREA</p>
      <label for="descripcion">Modifica la descripción de la tarea:</label>
      <input
        type="text"
        name="descripcion"        
        v-model="newTaskForm.desc"
      />
      <br />
      <label for="states">Estado de la tarea:</label>
      <select name="states" id="states" v-model="newTaskForm.state">
        <option v-for="state in statesTasks" :key="state">{{state}}</option>
      </select>

      <br />
      <div v-if="newTaskForm.state=='Finalizada'">
        <label for="createUser">Usuarios que cierra la tarea:</label>
        <select name="userChoices" id="userChoices" v-model="newTaskForm.close_user">
          <option v-for="user in users" :key="user.name">{{user.name}}</option>
        </select>
      </div>
      <button v-on:click="update">Cambiar</button>
    </div>
  </form>
</template>

<script>
export default {
  name: "FormTask",
  props: {
    taskToModify: Object
  },
  data() {
    return {
      newTaskForm: {
        desc: this.taskToModify.desc,
        create_date:this.taskToModify.create_date,
        create_user:this.taskToModify.create_user,       
        state: "",
        close_user: "",
      },
      users: JSON.parse(window.localStorage.getItem("users")),
      statesTasks: JSON.parse(window.localStorage.getItem("estados"))
    };
  },
  methods: {
   update:function(){
      this.$emit('updateDataTask',this.newTaskForm)
   }
}};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
.modal {
  display: block;
  position: fixed; /* Stay in place */
  z-index: 1; /* Sit on top */

  padding: 15% 25% 15% 25%;
  left: 0;
  top: 0;
  width: 50%; /* Full width */
  height: 100%; /* Full height */
  overflow: auto; /* Enable scroll if needed */
  background-color: rgb(0, 0, 0); /* Fallback color */
  background-color: rgba(0, 0, 0, 0.4); /* Black w/ opacity */
}
.modal-content {
  background-color: #fefefe;
  margin: auto;

  border: solid 0.5em #0090c5;
  border-radius: 6px;
  padding: 2em 2em 2em 2em;
  text-align: center;
}
</style>
