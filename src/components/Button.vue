<template>
  <button @click="onClick()" className="task-button">{{ text }}</button>
</template>

<script>
export default {
  name: "new-task-button",
  props: ["text"],

  methods: {
    onClick() {
      console.log("click");
    },
  },
};
</script>

<style lang="scss" scoped></style>
