<script lang="ts" setup>
import TaskForm from "./components/TaskForm.vue";
import { ref } from "vue";
import type { Task } from "./types";

const message = ref("Hello World");
const tasks = ref<Task[]>([
  {
    id: crypto.randomUUID(),
    title: "Sample Task 1",
    completed: false,
  },
  {
    id: crypto.randomUUID(),
    title: "Sample Task 2",
    completed: false,
  },
]);

const addTask = (newTask: string) => {
  tasks.value.push({
    id: crypto.randomUUID(),
    title: newTask,
    completed: false,
  });
};
</script>

<template>
  <main>
    <h1>{{ message }}</h1>

    <TaskForm @addTask="addTask" />

    <ul>
      <li v-for="task in tasks" :key="task.id">
        <label :for="task.id">
          <input type="checkbox" v-model="task.completed" />
          <span :class="{ completed: task.completed }">{{ task.title }}</span>
        </label>
      </li>
    </ul>
  </main>
</template>

<style>
main {
  max-width: 800px;
  margin: 1rem auto;
}

.button-container {
  display: flex;
  justify-content: end;
}

.completed {
  text-decoration: line-through;
}

ul {
  list-style: none;
  padding: 0;
  margin: 0;
}

li {
  display: flex;
  align-items: center;
  gap: 1rem;
}
</style>
