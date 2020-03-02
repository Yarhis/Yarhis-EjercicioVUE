<template>
   <!--<tr>
    <td v-for ="(value,key) in task " v-bind:key="key">

    {{value}}    
     </td>
     <td>
    <button v-on:click="modifyTask">modificar</button>
    </td>
    <td>
    <button  v-on:click="$emit('deleteTask')">borrar</button>
    </td>
    </tr> -->

    <tr>
   <td v-for ="(value,key) in newTask " v-bind:key="key">

    {{value}}    
     </td>
     <td>
    <button v-on:click="$emit('showForm',newTask)">modificar</button>
    </td>
    <td>
    <button  v-on:click="$emit('deleteTask')">borrar</button>
    </td>
    </tr>


    
</template>

<script>

// import FormTask from '@/components/FormTask.vue'

  
export default {
  name: 'Task',
  props: {
    task: Object
  },
  // components:{FormTask},
data() {
    return {
    newTask:"",
    // enabledForm: false
    }},
    methods: {
      modifyTask:function(){
        this.newTask= {
        desc: "prueba de cambio", 
        create_date:new Date(), 
        create_user: "usuario69", 
        state: "lalalalallaal", 
        close_user:null}

        
      }     
    }, 
    mounted() {
      this.newTask = this.task
    }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
