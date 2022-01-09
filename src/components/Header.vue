<template>
  <header>
      <h1>{{title}}
           <i class="fa fa-etsy" aria-hidden="true"></i>
      </h1>
     
      <Button class="btn" text="Add Task" color = "green"/>
     
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

