<script>
export default {
  name: "TaskComponent",
  props: {
    task: Object,
  },
  methods: {
    onDelete(id) {
      this.$emit("delete-task", id);
    }
  },
  emits: ["delete-task", "toggle-reminder"],
}
</script>

<template>
  <div :class="[task.reminder ? 'reminder' : '', 'task']" @dblclick="$emit('toggle-reminder', task.id)">
    <h3>{{ task.title }} <i class="fas fa-times" @click="onDelete(task.id)"></i></h3>
    <p>{{ task.day }}</p>
  </div>
</template>

<style scoped>
.task {
  background: #F4F4F4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}

.task.reminder {
  border-left: 5px solid green;
}

.task h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.fas {
  color: red;
}
</style>