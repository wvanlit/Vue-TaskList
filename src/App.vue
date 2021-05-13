<template>
  <div class="container">
    <Header
        :show-add-task="showAddTask"
        @add-task-clicked="this.showAddTask = !this.showAddTask"
    />
    <div v-show="showAddTask">
      <AddTask @add-task="addTask"/>
    </div>
    <Tasks
        :tasks="this.tasks"
        @delete-task="deleteTask"
        @toggle-reminder="toggleReminder"
    />
  </div>
</template>

<script>
import Header from "@/components/Header";
import Tasks from "@/components/Tasks";
import AddTask from "@/components/AddTask";

export default {
  name: 'App',
  components: {
    AddTask,
    Tasks,
    Header
  },
  data() {
    return {
      tasks: [],
      showAddTask: false,
    }
  },
  mounted() {
    if (localStorage.tasks) {
      try {
        this.tasks = JSON.parse(localStorage.getItem('tasks'));
      } catch (e) {
        localStorage.removeItem('tasks');
      }
    } else {

      this.tasks = []
      this.addTask({
        id: 0,
        text: 'Add more Tasks',
        day: 'now',
        reminder: false,
      })

    }
  },
  methods: {
    deleteTask(id) {
      if (confirm('Are you sure?')) {
        this.tasks = this.tasks.filter((task) => task.id !== id)
        this.persist()
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => task.id === id ? {...task, reminder: !task.reminder} : task)
      this.persist()
    },
    addTask(task) {
      this.tasks.push(task)
      this.persist()
    },
    persist() {
      const parsed = JSON.stringify(this.tasks)
      localStorage.setItem('tasks', parsed)
    }
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@300;400&display=swap');

* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: 'Poppins', sans-serif;
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
