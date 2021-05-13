<template>
  <header>
    <h1>Task Tracker</h1>
    <Button
        :color="showAddTask ? 'red' : 'green'"
        :text="showAddTask ? 'Close' : 'Add Task'"
        @add-task-clicked="$emit('add-task-clicked')"
    />
  </header>
</template>

<script>
import Button from "@/components/Button";

export default {
  name: "Header",
  components: {
    Button
  },
  props: {
    showAddTask: Boolean
  }
}
</script>

<style scoped>
header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
}
</style>