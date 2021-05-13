<template>
  <button :style="{background: color}" class="btn" @click="$emit('add-task-clicked')">{{ text }}</button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: {
      type: String,
      default: "Add Task"
    },
    color: {
      type: String,
      default: "green"
    },
  },
}
</script>

<style scoped>

</style>