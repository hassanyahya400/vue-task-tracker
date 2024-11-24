<script>
import Button from "@/components/Button.vue";

export default {
  name: "HeaderComponent",
  props: {
    title: {
      type: String,
      default: "Header Title"
    },
  },
  components: {
    Button,
  }
}
</script>

<template>
  <header>
    <h1>{{ title }}</h1>
    <Button name="Add Task" bg-color="green"/>
  </header>
</template>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>