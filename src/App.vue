<script>
import Header from "@/components/Header.vue";
import Tasks from "@/components/Tasks.vue";

export default {
  name: 'App',
  components: {
    Header,
    Tasks
  },
  data() {
    return {
      tasks: []
    }
  },
  methods: {
    deleteTask(id) {
      if (confirm("Are you sure?")) {
        console.log(id, "from App/js")
        this.tasks = this.tasks.filter((task) => task.id !== id)
      }
    },
    toggleReminder(id) {
      this.tasks = this.tasks.map((task) => {
        return (
            task.id === id ? {...task, reminder: !task.reminder} : task
        )
      })
    }
  },
  created() {
    this.tasks = [
      {
        "id": 1,
        "title": "Buy groceries for the week",
        "day": "Monday 2AM",
        "reminder": true
      },
      {
        "id": 2,
        "title": "Finish project report",
        "day": "Wednesday 10PM",
        "reminder": false
      },
      {
        "id": 3,
        "title": "Call Mom",
        "day": "Friday 12AM",
        "reminder": true
      }
    ]

  }
}
</script>

<template>
  <Header title="Task Tracker"/>
  <Tasks :tasks="tasks" @delete-task="deleteTask" @toggle-reminder="toggleReminder"/>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
