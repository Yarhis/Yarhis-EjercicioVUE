<template>
  <tr>
    <td>{{task.desc}}</td>
    <td><Timestamp v-bind:datetime="task.create_date"></Timestamp></td>
    <td>{{task.create_user}}</td>
    <td>{{task.state}}</td>
    <td>{{task.close_user}}</td>
    <td>
      <button v-on:click="$emit('showForm')">modificar</button>
    </td>
    <td>
      <button v-on:click="$emit('deleteTask')">borrar</button>
    </td>
  </tr>

   <!-- <tr>
    <td v-for="(value,key) in task " v-bind:key="key">{{value}}</td>
    <td>
      <button v-on:click="$emit('showForm')">modificar</button>
    </td>
    <td>
      <button v-on:click="$emit('deleteTask')">borrar</button>
    </td>
  </tr> -->
</template>

<script>

import Timestamp from '@/components/Timestamp.vue'

export default {
  name: "Task",
  components:{Timestamp},
  props: {
    task: Object
  },
  data() {
    return {
      newTask: ""
    };
  },
  methods: {
    // }
  },
  mounted() {
    // this.newTask = this.task
  }
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
