//App.vue

<template>
  <div class="container">
    <Header
      :showAddTask="showAddTask"
      @toggle-add-task="toggleAddTask"
      title="Task Tracker"
    />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask" />
    </div>
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
    AddTask,
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    };
  },
  emit: ["add-task"],
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },

    async deleteTask(id) {
      if (confirm("Are you sure you want to delete")) {

        const res = await fetch(`api/tasks/${id}`,{
          method:'delete'
        })

        res.status == 200 ? (this.tasks = this.tasks.filter((task) => task.id != id)):alert("Error Deleting Msg")
      }
    },
    async addTask(task) {

      //using post request add task method

      const res = await fetch('api/tasks',{
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(task),

      })

      console.log(res);

      const data = await res.json();
      this.tasks = [...this.tasks,data];

      // //spread across the current task and just add` new one on to items
      // this.tasks = [...this.tasks, task];
    },
    //updating a task by changing the reminder from either true to false or false to true
    //
    async toggleReminder(id) {

      const taskToToggle = await this.fetchTask(id);

      const updTask = {...taskToToggle,reminder:!taskToToggle.reminder}

      const res = await fetch(`api/tasks/${id}`,{
        method: "PUT",
        headers: { "Content-type": "application/json"},
        body: JSON.stringify(updTask)
      })

      const data =  await res.json();
      console.log("data.id",data.id);
      this.tasks = this.tasks.map(t => t.id == data.id ? {...t,reminder:data.reminder}:t)
      


      // this.tasks = this.tasks.map((task) =>
      //   //if the task .id  == to id that pass in
      //   task.id == id
      //     ? //if it is the what we want to return array of objects where we have the initial task properties  so we can spread across
      //       //the initial task , and change the reminder to  what ever the opposite current task reminder
      //       //else if it dose not match the id we want to do anting return initial task
      //       { ...task, reminder: !task.reminder }
      //     : task
      // );
    },

    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },

    async fetchTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },

  async created() {
    this.tasks = await this.fetchTasks();

    // this.tasks = [
    //   {
    //     id: 1,
    //     text: "222",
    //     day: "day",
    //     reminder: true,
    //   },
    //   {
    //     id: 2,
    //     text: "333",
    //     day: "day",
    //     reminder: false,
    //   },
    //   {
    //     id: 3,
    //     text: "dsds",
    //     day: "day",
    //     reminder: false,
    //   },
    //   {
    //     id: 4,
    //     text: "sdafas",
    //     day: "day",
    //     reminder: true,
    //   },
    // ];
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
