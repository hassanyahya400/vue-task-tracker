<script>
import Header from "@/components/Header.vue";
import Tasks from "@/components/Tasks.vue";
import AddTask from "@/components/AddTask.vue";

export default {
  name: 'App',
  components: {
    Header,
    Tasks,
    AddTask,
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
    },
    addNewTask(task) {
      this.tasks = [...this.tasks, task];
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
  <div>
    <Header title="Task Tracker"/>
    <AddTask @add-task="addNewTask"/>
    <Tasks :tasks="tasks" @delete-task="deleteTask" @toggle-reminder="toggleReminder"/>
  </div>
</template>

<style>
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
