<template>
  <div id="app">
    <div class="add-task">
      <input type="text" v-model="newTask" placeholder="Add New Task">
      <button @click="addTask">Add</button>
    </div>
    <div class="task-list">
      <ul>
        <li v-for="task in tasks" :key="task.id">
          <span>{{ task.name }}</span>
          <button @click="editTask(task)">Edit</button>
          <button @click="deleteTask(task.id)">Delete</button>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      newTask: '',
      tasks: []
    };
  },
  methods: {
    addTask() {
      if (this.newTask.trim()) {
        this.tasks.push({ id: Date.now(), name: this.newTask });
        this.newTask = '';
      }
    },
    editTask(task) {
      const newName = prompt('Enter new task name:', task.name);
      if (newName && newName.trim()) {
        task.name = newName.trim();
      }
    },
    deleteTask(taskId) {
      this.tasks = this.tasks.filter(task => task.id !== taskId);
    }
  }
};
</script>

<style scoped>
#app {
  font-family: Arial, sans-serif;
  max-width: 600px;
  margin: 0 auto;
  padding: 20px;
}

.add-task {
  display: flex;
  align-items: center;
  margin-bottom: 20px;
}

.add-task input[type="text"] {
  flex: 1;
  padding: 8px;
  margin-right: 10px;
}

.add-task button {
  padding: 8px 16px;
  background-color: #d6768f;
  color: white;
  border: none;
  cursor: pointer;
  transition: background-color 0.3s;
}

.add-task button:hover {
  background-color: #d6768f;
}

.task-list ul {
  list-style-type: none;
  padding: 0;
}

.task-list li {
  display: flex;
  align-items: center;
  margin-bottom: 10px;
}

.task-list span {
  flex: 1;
}

.task-list button {
  padding: 4px 8px;
  background-color: #8579d5;
  color: white;
  border: none;
  cursor: pointer;
  margin-left: 5px;
  transition: background-color 0.3s;
}

.task-list button:hover {
  background-color: #8579d5;
}
</style>