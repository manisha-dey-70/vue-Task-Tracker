<template>
  <header class="row-flex justify-sb">
    <h1>{{ title }}</h1>
    <Button
      v-show="homePage"
      @btn-click="$emit('toggle-add-task')"
      :text="showAddTask ? 'Close' : 'Add task'"
      :color="showAddTask ? 'blue' : 'green'"
    />
  </header>
</template>

<script>
import Button from "./Button.vue";
export default {
  name: "Header",
  props: {
    title: {
      type: String,
      default: "Hello", // if you don't pass a prop it will take the default prop
    },
    showAddTask: {
      type: Boolean,
    },
  },
  components: {
    Button,
  },
  computed: {
    homePage() {
      // alert(this.$route.path);
      if (this.$route.path === "/") {
        return true;
      } else {
        return false;
      }
    },
  },
};
</script>

<style scoped>
/* header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 20px;
} */
</style>
