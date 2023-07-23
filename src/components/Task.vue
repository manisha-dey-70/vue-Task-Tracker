<template>
  <div
    @dblclick="onToggleReminder(task.id)"
    :class="[task.reminder ? 'reminder' : '', 'task col-flex']"
  >
    <h3 class="row-flex justify-sb">
      {{ task.text }}
      <i @click="onDelete(task.id)" class="fas fa-times"></i>
    </h3>

    <div class="row-flex justify-start">{{ task.day }}</div>
  </div>
</template>

<script>
export default {
  name: "Task",
  props: {
    task: { type: Object },
  },
  methods: {
    onDelete(id) {
      this.$emit("delete-task", id);
    },
    onToggleReminder(id) {
      this.$emit("toggle-reminder", id);
    },
  },
};
</script>

<style scoped>
.task {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  cursor: pointer;
}
.reminder {
  border-left: 4px solid green;
}
i {
  color: #e80000;
}
</style>
