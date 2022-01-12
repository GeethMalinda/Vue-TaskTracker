// Tasks.vue


<template>
  <div  v-for="task in tasks" :key="task.id">
  <!-- <h3>{{task.text}}</h3> -->
  <Task @delete-task="$emit('delete-task',task.id)"  @toggle-reminder ="$emit('toggle-reminder',task.id)" :task="task"/>
  </div>
</template>

<script>
import Task from './Task'

export default {
    name:"Tasks",
    props: {
        tasks:Array,
    },
    components: {
      Task,
    },
    emit:["delete-task","toggle-reminder"]
}
</script>

<style>

</style>