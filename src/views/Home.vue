<script>
import Tasks from "@/components/Tasks.vue";
import AddTask from "@/components/AddTask.vue";

export default {
  name: "HomePage",
  props: { showAddTask: Boolean },
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return {
      tasks: [],
    };
  },
  methods: {
    async deleteTask(id) {
      if (confirm("Are you sure?")) {
        const res = await fetch(`api/tasks/${id}`, {
          method: "DELETE",
        });

        res.statusText == "OK"
          ? (this.tasks = this.tasks.filter((task) => task.id !== id))
          : alert("an error occured while deleting the task");
      }
    },
    async toggleReminder(id) {
      const task = await this.fetchTaskById(id);
      const updTask = { ...task, reminder: !task.reminder };

      const res = await fetch(`api/tasks/${id}`, {
        method: "PUT",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(updTask),
      });

      const data = res.json();

      res.statusText == "OK"
        ? (this.tasks = this.tasks.map((task) => {
            return task.id === id ? { ...task, reminder: data.reminder } : task;
          }))
        : alert("an error occured while setting the reminder");
    },
    async addNewTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();
      this.tasks = [...this.tasks, data];
    },
    
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    async fetchTaskById(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();
      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>

<template>
  <AddTask v-show="showAddTask" @add-task="addNewTask" />

  <Tasks
    :tasks="tasks"
    @delete-task="deleteTask"
    @toggle-reminder="toggleReminder"
  />
</template>

<style scoped></style>
