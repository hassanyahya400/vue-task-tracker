<script>
export default {
  name: "ButtonComponent",
  props: {
    name: String,
    bgColor: String,
  },
  methods: {
    onClick() {
      console.log("clicked me!")
    }
  }
}
</script>

<template>
  <button :style="{background: bgColor}" class="btn" @click="onClick()">{{ name }}</button>
</template>

<style scoped>

</style>