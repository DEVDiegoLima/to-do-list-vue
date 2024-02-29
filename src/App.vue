<template>
  <div class="container">
    <div class="task-container">
      <Header />
      <main>
        <TaskEntry @task-added="addTaskToList" />
        <ul>
          <List
            v-for="(task, index) in tasks"
            :key="index"
            :task="task"
            @delete-task="deleteTask"
            @edit-task="editTask"
          />
        </ul>
      </main>
    </div>
  </div>
</template>

<script setup>
import { onMounted, ref } from "vue";
import Header from "./components/Header.vue";
import TaskEntry from "./components/TaskEntry .vue";
import List from "./components/List.vue";

const tasks = ref([]);
const addTaskToList = (task) => {
  tasks.value.push(task);
  saveTasksToLocalStorage();
};

const deleteTask = (taskToDelete) => {
  const indexToDelete = tasks.value.findIndex((task) => task === taskToDelete);
  if (indexToDelete !== -1) {
    tasks.value.splice(indexToDelete, 1);
    saveTasksToLocalStorage();
  }
};

const editTask = ({ oldTask, newTask }) => {
  const indexToEdit = tasks.value.findIndex((task) => task === oldTask);
  if (indexToEdit !== -1) {
    tasks.value[indexToEdit] = newTask;
    saveTasksToLocalStorage();
  }
};

const saveTasksToLocalStorage = () => {
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
};

const loadTasksFromLocalStorage = () => {
  const storedTasks = localStorage.getItem("tasks");
  if (storedTasks) {
    tasks.value = JSON.parse(storedTasks);
  }
};

onMounted(() => {
  loadTasksFromLocalStorage();
});
</script>

<style scoped>
.task-container {
  height: auto;
  width: 600px;
  background-color: #262e4c;
  border-radius: 10px 10px 0 0;
}
</style>
