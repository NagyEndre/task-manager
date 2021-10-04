<template>
  <div id="app">
    <header class="container">
      <h1>Task Manager</h1>
    </header>
    <section class="container">
      <h2>Today's TODOs</h2>
      <form id="controlls" @submit.prevent="addTask">
        <input type="text" name="" id="" v-model.trim="currentTask" />
        <button type="submit">ADD</button>
      </form>
      <p v-if="tasks.length === 0">
        No todos have been added yet. Please start adding one.
      </p>
      <ul v-else>
        <li
          v-for="(task, index) in tasks"
          :key="index"
          @click="removeTask(index)"
        >
          {{ task }}
        </li>
      </ul>
    </section>
  </div>
</template>

<script lang="ts">
import { Component, Vue } from "vue-property-decorator";

@Component
export default class App extends Vue {
  tasks: string[] = [];
  currentTask: null | string = null;

  addTask(): void {
    if (this.currentTask) {
      this.tasks.unshift(this.currentTask);
      this.currentTask = null;
    }
  }
  removeTask(index: number): void {
    this.tasks.splice(index, 1);
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
}
section {
  background-color: white;
}
button {
  background-color: steelblue;
  color: white;
  cursor: pointer;
  padding: 0.05rem 1rem;
  box-shadow: 1px 1px 4px rgba(0, 0, 0, 0.26);
  height: 100%;
  width: 10%;
}
li {
  list-style: none;
  background-color: green;
  margin: 1rem;
  padding: 0.5rem;
  border-radius: 1rem;
  color: white;
  font-size: 1.5rem;
}
input {
  border: 1px solid #ccc;
  font: inherit;
  height: 100%;
  width: 70%;
}
</style>
