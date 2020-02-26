<template>
  <div class="task">
   <span v-for ="(value,key) in task " v-bind:key="key">

     {{key}} : {{value}}
   </span>
   
      
  </div>

</template>

<script>
export default {
  name: 'Task',
  props: {
    task: Object
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>


</style>
