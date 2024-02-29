<template>
  <div class="input-group">
    <input
      type="text"
      placeholder="add new Task..."
      id="inputTask"
      v-model="newTask"
    />
    <button class="btn" @click="addTask">
      <i class="fa-solid fa-plus"></i>
    </button>
  </div>
</template>

<script>
import "@fortawesome/fontawesome-free/css/all.css";
export default {
  name: "TaskEntry",
  data() {
    return {
      newTask: "",
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.$emit("task-added", this.newTask);
        this.newTask = "";
      }
    },
  },
};
</script>
<style scoped>
.input-group {
  display: inline-flex;
  width: 100%;
}
#inputTask {
  height: 50px;
  width: 100%;
  padding: 15px;
  font-size: 20px;
  background-color: #3c4979;
  color: #ffffff;
  border: none;
}

.btn {
  height: auto;
  width: 60px;
  background-color: #1dd2af;
  border: none;
  cursor: pointer;
  color: #ffffff;
  font-size: 20px;
}
</style>
