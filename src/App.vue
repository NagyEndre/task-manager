<template>
  <div id="app">
    <header class="container">
      <h1>Task Manager</h1>
    </header>
    <section class="container">
      <h2>Today's tasks</h2>
      <form id="controlls" @submit.prevent="addTask">
        <input type="text" name="" id="" v-model.trim="currentTask" />
        <button type="submit" class="btn-primary">Add</button>
      </form>
      <p v-if="tasks.length === 0">
        No tasks have been added yet. Start adding one.
      </p>
      <transition-group
        tag="ul"
        name="todo-list"
        v-show="isListVisible"
        @after-leave="console.log('after-leave')"
      >
        <li v-for="(task, index) in tasks" :key="index">
          {{ task }}
          <img
            src="..\src\assets\x-circle-fill.svg"
            class="x-circle-fill"
            @click="removeTask(index)"
          />
        </li>
      </transition-group>
      <button
        v-if="tasks.length > 0"
        @click="toggleListDisplay"
        class="btn-primary"
      >
        <span v-if="isListVisible">Hide</span><span v-else>Show</span> List
      </button>
    </section>
    <PopupDialog :open="error">
      <h2>Invalid task</h2>
      <p>Task title must not be empty!</p>
      <button @click="acknowledgeError">OK</button>
    </PopupDialog>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";
import PopupDialog from "./components/PopupDialog.vue";

@Component({ components: { PopupDialog } })
export default class App extends Vue {
  tasks: string[] = [];
  currentTask: null | string = null;
  isListVisible = true;
  error = false;

  addTask(): void {
    if (this.currentTask) {
      this.tasks.push(this.currentTask);
      this.currentTask = null;
    } else {
      this.error = true;
    }
  }
  removeTask(index: number): void {
    this.tasks.splice(index, 1);
  }
  toggleListDisplay() {
    this.isListVisible = !this.isListVisible;
  }
  acknowledgeError() {
    this.error = false;
  }
}
</script>

<style>
* {
  box-sizing: border-box;
}
body {
  background-color: whitesmoke;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
header {
  background-color: darkgreen;
  color: white;
  padding: 1rem;
}
.container {
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
  width: 75%;
  margin: 1rem auto;
  border-radius: 1rem;
  padding: 1rem;
}
#controlls {
  height: 2rem;
  margin-bottom: 2rem;
}
section {
  background-color: white;
}
.btn-primary {
  font-size: 1rem;
  background-color: steelblue;
  color: white;
  cursor: pointer;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
  padding: 0.5rem 1rem;
  border-radius: 0.5rem;
}
.x-circle-fill {
  height: 1.3rem;
  margin: 0;
  padding: 0;
  position: absolute;
  right: 0.8rem;
}
li {
  list-style: none;
  background-color: green;
  margin: 1rem;
  padding: 0.5rem;
  border-radius: 1rem;
  color: white;
  font-size: 1.5rem;
  position: relative;
}
input {
  border: 1px solid #ccc;
  font: inherit;
  height: 100%;
  width: 70%;
}

.todo-list-enter {
  opacity: 0;
  transform: translateX(-50px);
}
.todo-list-leave-active,
.todo-list-enter-active {
  transition: all 0.3s ease-out;
}
.todo-list-leave .todo-list-enter-to {
  opacity: 1;
  transform: translate(0);
}
.todo-list-leave-to {
  opacity: 0;
  transform: translateX(50px);
}
</style>
