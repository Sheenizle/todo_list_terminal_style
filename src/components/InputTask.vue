<template>
  <input
    class="addInput"
    placeholder="Писать сюда"
    v-model="taskAdd"
    @keyup.enter="submitTask(taskAdd)"
  />
  <button class="addBut" @click="submitTask(taskAdd)">ADD</button>
</template>

<script>
export default {
  name: "InputTask",
  data: () => ({
    taskAdd: "",
  }),
  methods: {
    submitTask(task) {
      if (task === "") {
        return;
      }
      this.$emit("InputTask", {
        title: task,
        id: Date.now(),
        done: false,
      });
      this.taskAdd = "";
    },
  },
};
</script>
