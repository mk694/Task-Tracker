<template>
  <div
    @dblclick="$emit('toggle-reminder', task.id)"
    :class="['task-container', task.reminder ? 'reminder' : '']"
    v-for="task in tasks"
    :key="task.id"
  >
    <Task @remove-task="$emit('remove-task', task.id)" :task="task" />
  </div>
</template>

<script>
import Task from "./Task.vue";
export default {
  name: "all_tasks",
  props: {
    tasks: Array,
    task: Object,
  },
  components: { Task },

  emits: ["remove-task", "toggle-reminder"],
};
</script>

<style lang="scss" scoped>
.task-container {
  background-color: #e3e3e3;
  padding: 16px;
  padding-left: 20px;
  margin: 5px;
  border-radius: 10px;
  cursor: pointer;

  &.reminder {
    border-left: 4px solid green;
    border-bottom-left-radius: 0px;
    border-top-left-radius: 0px;
    padding-left: 16px;
  }
}
</style>
