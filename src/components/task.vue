<template>
  <div class="tasks">
    <input v-if="active" v-model="edit" />
    <div
      v-else
      class="singleTask"
      :class="{
        done: task.done === true,
      }"
    >
      {{ task.title }}
    </div>
    <button class="btn" @click="$emit('complited-task', { id: task.id })" v-if="!task.done">
      ✅
    </button>
    <button class="btn" @click="active = true" v-if="!active">✏️</button>
    <button
      v-if="active"
      class="btn"
      @click="handleSave({ edit, id: task.id })"
    >
      💾
    </button>
    <button class="btn" @click="$emit('remove-task', task)">❌</button>
  </div>
</template>

<script>
/*
  {
    title: '',
    id: 0,
    done: false,
  }  
  */
export default {
  name: "task",
  props: {
    task: {
      type: Object,
      default: () => {},
    },
    index: Number,
  },
  data: (component) => ({
    active: false,
    edit: component.task.title,
  }),
  methods: {
    handleSave({ edit, index }) {
      this.$emit("save-task", { edit, index });
      this.active = false;
    },
  },
};
</script>

<style>
.tasks {
  display: flex;
}

.done {
  text-decoration: line-through white;
}

.singleTask {
  border: 1px outset silver;
  border-radius: 5px;
  margin-left: 10px;
  margin: 3px;
  padding: 3px;
  text-align: left;
  width: 100%;
}

.btn {
  margin: 3px;
  background-color: #252526;
}

.btn:hover {
  background-color: #4dacf2;
}
</style>
