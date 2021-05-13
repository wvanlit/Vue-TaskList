<template>
  <form class="add-form" @submit="onSubmit">
    <div class="form-control">
      <label>Task</label>
      <input
          v-model="text"
          name="task"
          placeholder="Add Task"
          type="text"
      />
    </div>
    <div class="form-control">
      <label>Day & Time</label>
      <input
          v-model="day"
          name="day"
          placeholder="Add Day & Time"
          type="text"
      />
    </div>
    <div class="form-control form-control-check">
      <label>Set Reminder</label>
      <input
          v-model="reminder"
          name="reminder"
          type="checkbox"/>
    </div>
    <input
        class="btn btn-block"
        type="submit"
        value="Save Task"
    />
  </form>
</template>

<script>
export default {
  name: "AddTask",
  data() {
    return {
      text: '',
      day: '',
      reminder: false,
    }
  },
  methods: {
    onSubmit(e) {
      e.preventDefault()
      if (!this.text) {
        alert('Please add text to your task')
      }

      const newTask = {
        id: Math.floor(Math.random() * 10000),
        text: this.text,
        day: this.day,
        reminder: this.reminder
      }

      this.text = ''
      this.day = ''
      this.reminder = false

      this.$emit('add-task', newTask)
    }
  }
}
</script>

<style scoped>
.add-form {
  margin-bottom: 40px;
}

.form-control {
  margin: 20px 0;
}

.form-control label {
  display: block;
}

.form-control input {
  width: 100%;
  height: 40px;
  margin: 5px;
  padding: 3px 7px;
  font-size: 17px;
}

.form-control-check {
  display: flex;
  align-items: center;
  justify-content: space-between;
}

.form-control-check label {
  flex: 1;
}

.form-control-check input {
  flex: 2;
  height: 20px;
}
</style>