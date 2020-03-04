<template>
 
   <tr>
    <td v-for="(value,key) in task " v-bind:key="key">{{value}}</td>
    <td>
      <button v-on:click="$emit('showForm')">modificar</button>
    </td>
    <td>
      <button v-on:click="$emit('deleteTask')">borrar</button>
    </td>
  </tr>
</template>

<script>


export default {
  name: "Task",
  props: {
    task: Object
  },
  data() {
    return {
    };
  },
  methods: {

  },
  mounted() {
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
tr, td{
  background-color: rgb(236, 161, 62);
 border-radius: 8px;
 padding: 10px 15px 10px 15px;
 color: rgb(255, 255, 255);
   font-weight: bold;

}

button{
  background-color: rgb(255, 255, 255);
  color: rgb(236, 161, 62);
}
</style>
