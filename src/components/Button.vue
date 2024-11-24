<script>
export default {
  name: "ButtonComponent",
  props: {
    name: String,
    bgColor: String,
  },
  methods: {
    onClick() {
      this.$emit("on-button-click")
    }
  }
}
</script>

<template>
  <button :style="{background: bgColor}" class="btn" @click="onClick()">{{ name }}</button>
</template>

<style scoped>

</style>