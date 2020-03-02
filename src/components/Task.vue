<template>
   <tr>
   <td v-for ="(value,key) in task " v-bind:key="key">

    {{value}}    
     </td>
     <td>
    <button>modificar</button>
    </td>
    <td>
    <button  @click="$emit('deleteTask')">borrar</button>
    </td>
    </tr>
<!-- <span v-for ="(value,key) in task " v-bind:key="key">

     {{key}} : {{value}}
    
     </span>
    <button>modificar</button>
    <button >borrar</button>  
    
    @click="removeTodo(task)"-->


</template>

<script>
export default {
  name: 'Task',
  props: {
    task: Object
  },
  
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
