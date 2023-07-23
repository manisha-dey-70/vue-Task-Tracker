<template>
  <button
    @click="onClick()"
    :style="{ background: color, color: ' white ' }"
    class="btn"
  >
    {{ text }}
  </button>
</template>

<script>
export default {
  name: "Button",
  props: {
    text: { type: String, default: "Add" },
    color: { type: String, default: "red" },
  },
  methods: {
    onClick() {
      this.$emit("btn-click");
    },
  },
};
</script>

<style scoped>
.btn {
  border: none;
  cursor: pointer;
  margin: 25px 0;
  padding: 0 20px;
  border-radius: 4px;
}
</style>
