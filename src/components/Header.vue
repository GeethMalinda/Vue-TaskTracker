<template>
  <header>
      <h1>{{title}}</h1>
      <Button class="btn" text="Add Task" color = "green"/>
      <Button class="btn" text="Update Task" color = "blue"/>
      <Button class="btn" text="Delete Task" color = "orange"/>

  </header>
</template>

<script>
import Button from './Button'
export default {
    name:'Header',
    props:{
        title:{
            type: String,
            default:"Default"

        } 
    },
    components:{
        Button
    }
}
</script>

<style scoped>

header{
    display:flex;
    justify-content:center;
    margin-bottom:20px;
    align-items:center;
}
</style>>

