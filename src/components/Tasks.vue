<script>
import Task from './Task.vue'

export default {
  name: "TasksComopnent",
  props: {
    tasks: Array
  },
  components: {
    Task
  },
  emits: ["delete-task", "toggle-reminder"]
}
</script>

<template>
  <div>
    <Task v-for="task in tasks" :key="task.id" :task="task" @delete-task="this.$emit('delete-task',task.id)"
          @toggle-reminder="$emit('toggle-reminder', task.id)" />
  </div>
</template>

<style scoped>

</style>