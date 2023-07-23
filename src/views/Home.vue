<template>
  <div v-show="showAddTask"><AddTask @add-task="addTask" /></div>

  <Tasks
    @toggle-reminder="toggleReminder"
    @delete-task="deleteTask"
    :tasks="tasks"
  />
</template>

<script>
import Tasks from "../components/Tasks.vue";
import AddTask from "../components/AddTask.vue";

export default {
  name: "Home",
  props: {
    showAddTask: {
      type: Boolean,
    },
  },
  components: {
    Tasks,
    AddTask,
  },
  data() {
    return { tasks: [] };
  },
  methods: {
    async deleteTask(id) {
      if (confirm("Do you want to delete this task?")) {
        const res = await fetch(`api/tasks/${id}`, { method: "DELETE" });
        if (res.status === 200) {
          this.tasks = this.tasks.filter((task) => task.id !== id);
          setTimeout(() => {
            alert("Your task has been deleted!");
          }, 300);
        } else {
          alert("Some error occured, please try again!");
        }
      }
    },
    async toggleReminder(id) {
      if (confirm("Do you want to set a reminder for this task?")) {
        const reqTask = await this.fetchUniqueTask(id);

        const updatedTask = { ...reqTask, reminder: !reqTask.reminder };

        const res = await fetch(`api/tasks/${id}`, {
          method: "PUT",
          headers: { "Content-type": "application/json" },
          body: JSON.stringify(updatedTask),
        });

        const data = await res.json();

        this.tasks = this.tasks.map((task) =>
          task.id === id ? { ...task, reminder: data.reminder } : task
        );
      }
    },
    async addTask(task) {
      const res = await fetch("api/tasks", {
        method: "POST",
        headers: {
          "Content-type": "application/json",
        },
        body: JSON.stringify(task),
      });
      const data = await res.json();
      this.tasks = [...this.tasks, data];
      setTimeout(() => {
        alert("Your task has been added!");
      }, 300);
    },
    async fetchTasks() {
      const res = await fetch("api/tasks");
      const data = await res.json();
      return data;
    },
    async fetchUniqueTask(id) {
      const res = await fetch(`api/tasks/${id}`);
      const data = await res.json();

      return data;
    },
  },
  async created() {
    this.tasks = await this.fetchTasks();
  },
};
</script>
