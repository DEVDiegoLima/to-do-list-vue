<template>
  <li>
    <input type="radio" name="" id="" />
    <span v-if="!editing" @dblclick="startEditing">{{ task }}</span>
    <input
      class="task-editor"
      type="text"
      v-model="editedTask"
      v-if="editing"
      @keydown.enter.prevent="saveTask"
      @blur="cancelEditing"
    />
    <div class="button-container">
      <button class="btn-pencil" @click="startEditing">
        <i class="fa-regular fa-pen-to-square"></i>
      </button>
      <button class="btn-trash" @click="deleteTask">
        <i class="fa-regular fa-trash-can"></i>
      </button>
    </div>
  </li>
</template>

<script>
import "@fortawesome/fontawesome-free/css/all.css";
export default {
  name: "List",
  props: {
    task: {
      type: String,
      default: () => [],
    },
  },
  data() {
    return {
      editing: false,
      editedTask: this.task,
    };
  },
  methods: {
    deleteTask() {
      this.$emit("delete-task", this.task);
    },
    startEditing() {
      this.editing = true;
    },
    saveTask() {
      console.log("Salvando tarefa...");
      this.$emit("edit-task", { oldTask: this.task, newTask: this.editedTask });
      this.editing = false;
    },
    cancelEditing() {
      this.editing = false;
      this.editedTask = this.task;
    },
  },
};
</script>

<style scoped>
li {
  width: 100%;
  height: 50px;
  color: #fff;
  display: flex;
  justify-content: start;
  align-items: center;
  font-size: 18px;
  text-transform: capitalize;
  border-bottom: 0.1px solid rgba(255, 255, 255, 0.625);
}
li:last-child {
  border: none;
}
input[type="radio"] {
  margin: 0 10px;
  cursor: pointer;
}
input[type="radio"]:checked {
  background-color: #1dd2af;
}

li input[type="radio"]:checked + span {
  text-decoration: line-through;
  color: #ccc;
}

.button-container {
  display: flex;
  margin-left: auto;
}

.btn-pencil,
.btn-trash {
  font-size: 20px;
  background: transparent;
  border: none;
  color: #fff;
  cursor: pointer;
  transition: 0.2s color;
  padding: 0px 10px;
}

.btn-trash:hover {
  color: #de3f53;
}

.btn-pencil:hover {
  color: #1dd2af;
}

.task-editor {
  height: 50px;
  background-color: #262e4c;
  color: #fff;
  padding: 10px;
  width: 100%;
  border: none;
  outline: none;
  font-size: 18px;
}
</style>
