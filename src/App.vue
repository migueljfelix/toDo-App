<template>
  <div class="container">
    <Header title="To do List" />
    <div>
      <AddTask @add-task="addTask" />
    </div>
    <Tasks
      @toggle-completed="toggleCompleted"
      @delete-task="deleteTask"
      :tasks="tasks"
    />
  </div>
</template>

<script>
import Header from "./components/Header";
import Tasks from "./components/Tasks";
import AddTask from "./components/AddTask";

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
    };
  },
  methods: {
    addTask(task) {
      this.tasks = [task, ...this.tasks];
    },

    deleteTask(id) {
      this.tasks = this.tasks.filter((task) => task.id !== id);
    },

    toggleCompleted(id) {
      //updating a task by seting a reminder to false or true| return array of updated tasks
      // if for each task - fech if task.id is equal to the id passed in. if it is, return array of object where we have the enitial taskproprety and change the reminder to wathever the oposite the current task reminder, else if it doesnt match the id, do nothing.
      this.tasks = this.tasks.map((task) =>
        task.id === id ? { ...task, completed: !task.completed } : task
      );
    },
    //tasks fetch
    async fetchTasks() {
      const requestOptions = {
        method: "GET",
        headers: { "Content-Type": "application/json" },
        redirect: "follow",
      };
      const res = await fetch(
        "https://63650452f711cb49d1f2b256.mockapi.io/api/v1/tasks?sortBy=createdAt&order=desc&page=1&limit=10",
        requestOptions
      );
      const data = await res.json();
      return data;
    },
  },

  //calling fetch when component mounts
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<style lang="scss">

// soft reset 
body,
html,
#root {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  font-family: Roboto, sans-serif;
  font-weight: bold;
  background: linear-gradient(to right, #00aaff, #00ff6c);
}

// app Ui 
.container {
  max-width: 500px;
  margin: 30px auto;
  overflow: auto;
  min-height: 300px;
  padding: 30px;
  border-radius: 8px;
  background-color: rgba(246, 255, 247, 0.08);
}


</style>
