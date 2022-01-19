<template>
  <header>
    <h1>
      {{ title }}
      <i class="fa fa-etsy" aria-hidden="true"></i>
    </h1>

    <Button
      @btn-click="$emit('toggle-add-task')"
      class="btn"
      :text="showAddTask ? 'Close' : 'Add Task'"
      :color="showAddTask ? 'red' : 'green'"
    />
  </header>
</template>

<script>
import Button from "./Button";
export default {
  name: "Header",
  props: {
    showAddTask: Boolean,
    title: {
      type: String,
      default: "Default",
    },
  },
  components: {
    Button,
  },
};
</script>

<style scoped>
header {
  display: flex;
  justify-content: center;
  margin-bottom: 20px;
  align-items: center;
}
</style>>

