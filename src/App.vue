//App.vue

<template>
  <div class="container">
    <Header title="Task Tracker" />
    <AddTask @add-task= "addTask"/>
    <Tasks
      @toggle-reminder="toggleReminder"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
//import component
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";

//register the component
export default {
  name: "App",
  components: {
    Header,
    Tasks,
    AddTask
  },
  data() {
    return {
      tasks: [],
    };
  },
  emit:['add-task'],
  methods: {
    deleteTask(id) {
      if (confirm("Are you sure you want to delete")) {
        this.tasks = this.tasks.filter((task) => task.id != id);
      }
    },
    addTask(task){
      //spread across the current task and just add new one on to items
      this.tasks = [...this.tasks,task]
    },
    //updating a task by changing the reminder from either true to false or false to true
    //
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) =>
        //if the task .id  == to id that pass in
        task.id == id
          ? //if it is the what we want to return array of objects where we have the initial task properties  so we can spread across
            //the initial task , and change the reminder to  what ever the opposite current task reminder
            //else if it dose not match the id we want to do anting return initial task
            { ...task, reminder: !task.reminder }
          : task
      );
    },
  },

  created() {
    this.tasks = [
      {
        id: 1,
        text: "222",
        day: "day",
        reminder: true,
      },
      {
        id: 2,
        text: "333",
        day: "day",
        reminder: false,
      },
      {
        id: 3,
        text: "dsds",
        day: "day",
        reminder: false,
      },
      {
        id: 4,
        text: "sdafas",
        day: "day",
        reminder: true,
      },
    ];
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap");

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}
body {
  font-family: "Poppins", sans-serif;
}
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  border: 1px solid steelblue;
  padding: 30px;
  border-radius: 5px;
}
.btn {
  display: inline-block;
  background: #000;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;
}
.btn:focus {
  outline: none;
}
.btn:active {
  transform: scale(0.98);
}
.btn-block {
  display: block;
  width: 100%;
}
</style>
