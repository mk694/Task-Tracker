<template>
  <header>
    <h1>
      {{ title }}
    </h1>

    <Button text="Add new task" />
  </header>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "app-header",
  props: ["title", "text"],
  components: { Button },
};
</script>

<style scoped lang="scss">
button {
  display: inline-block;
  background: green;
  color: #fff;
  border: none;
  padding: 10px 20px;
  margin: 5px;
  border-radius: 5px;
  cursor: pointer;
  text-decoration: none;
  font-size: 15px;
  font-family: inherit;

  &:focus {
    outline: none;
  }
  &:active {
    transform: scale(0.98);
  }
}
</style>
