<template>
  <div class="container">
    <Header
      @toggle-add-task="toggleAddTask"
      :title="'Task Tracker'"
      :showAddTask="showAddTask"
    />
    <router-view :showAddTask="showAddTask"></router-view>
    <Footer />
  </div>
</template>

<script>
import Header from "./components/Header.vue";
import Footer from "./components/Footer.vue";

export default {
  name: "App",
  components: { Header, Footer },

  data() {
    return { showAddTask: false };
  },
  methods: {
    toggleAddTask() {
      this.showAddTask = !this.showAddTask;
    },
  },
};
</script>

<style>
#app {
  justify-content: center;
  display: flex;
}
.container {
  width: 50%;
  border: 1px solid black;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  padding: 20px;
  border-radius: 4px;
}
.justify-center {
  justify-content: center;
}
.justify-start {
  justify-content: flex-start;
}
.justify-sb {
  justify-content: space-between;
}
.row-flex {
  display: flex;
}
.col-flex {
  display: flex;
  flex-direction: column;
}
.align-center {
  align-items: center;
}
</style>
