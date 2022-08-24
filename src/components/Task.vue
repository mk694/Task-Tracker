<template>
  <h3>
    {{ task.text }}
    <i @click="$emit('remove-task')" class="fas fa-times"></i>
  </h3>
  <p>{{ task.day }}</p>
</template>

<script>
export default {
  name: "task-item",
  props: {
    task: Object,
  },

  methods: {},
  emits: ["remove-task"],
};
</script>

<style lang="scss" scoped>
h3 {
  display: flex;
  justify-content: space-between;
  align-items: center;
}
p,
h3 {
  user-select: none;
}
i {
  color: red;
  cursor: pointer;
  transition: all 0.2s;
  padding: 4px;
  &:active {
    transform: scale(0.9);
  }
}
</style>
