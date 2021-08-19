<template>
  <h2>{{ logo }}</h2>
  <h1>My first TO-DO list</h1>

  <div class="taskBoxes">
    <task
      v-for="(task, index) in list"
      :key="index"
      :task="task"
      @remove-task="removeFromlist"
      :index="index"
      @save-task="saveEditTask"
      @complited-task="complitTask"
    ></task>
  </div>
  <hr />
  <input-task @input-task="addToList" />
</template>

<script>
import task from "./components/task.vue";
import InputTask from "./components/InputTask.vue";
export default {
  components: {
    task: task,
    InputTask: InputTask,
  },
  data: () => ({
    list: [],
    logo: "<ICWT/>",
  }),
  mounted() {
    this.list = JSON.parse(localStorage.getItem("tasks")) || [];
  },
  methods: {
    addToList(task) {
      this.list.push(task);
      this.setToLocalStorage();
    },
    removeFromlist(task) {
      this.list = this.list.filter((taskDel) => task !== taskDel);
      this.setToLocalStorage();
    },
    setToLocalStorage() {
      localStorage.setItem("tasks", JSON.stringify(this.list));
    },
    saveEditTask({ edit, index }) {
      this.list[index] = edit;
      this.setToLocalStorage();
    },
    complitTask(task) {
      console.log(task);
      this.list = this.list.map((currentTask) => {
        console.log(currentTask.id);
        if (currentTask.id === task.id) {
          currentTask.done = true;
        }
        return currentTask;
      });
      this.setToLocalStorage();
    },
  },
};
</script>

<style>
html,
body {
  background-color: #252526;
}

h1 {
  color: #dcdcaa;
}

#app {
  font-family: "Source Code Pro", monospace;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #4dacf2;
  margin: 10px;
  padding: 20px;
  text-align: center;
  border: 1px solid silver;
  border-radius: 10px;
  background-color: #1e1e1e;
}

.taskBoxes {
  display: flex;
  flex-direction: column-reverse;
  width: 100%;
}

.addInput {
  background-color: #252526;
  width: 100%;
  color: #4dacf2;
}

.addBut {
  background-color: #252526;
  color: #c586c0;
  width: 100%;
}

.addBut:hover {
  background-color: #4dacf2;
  color: white;
}
</style>
