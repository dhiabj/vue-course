<script setup>
import { ref, onMounted } from 'vue';

/*export default {
  // Options API
  data () {
    return {
      name: 'John Doe',
      status: 'pending',
      tasks: ['Task 1', 'Task 2', 'Task 3'],
      link: 'https://www.google.com'
    }
  },
  methods: {
    toggleStatus () {
      if (this.status === 'active') {
        this.status = 'pending'
      } else if (this.status === 'pending') {
        this.status = 'active'
      } else {
        this.status = 'active'
      }
    }
  }
}*/

// Composition API
const name = ref('John Doe');
const status = ref('active');
const tasks = ref(['Task 1', 'Task 2', 'Task 3']);
const newTask = ref('');

const toggleStatus = () => {
  if (status.value === 'active') {
    status.value = 'pending';
  } else if (status.value === 'pending') {
    status.value = 'active';
  } else {
    status.value = 'active';
  }
};

const addTask = () => {
  if (newTask.value.trim() !== '') {
    tasks.value.push(newTask.value);
    newTask.value = '';
  }
};

const deleteTask = (index) => {
  tasks.value.splice(index, 1);
};

onMounted(async () => {
  try {
    const response = await fetch('https://jsonplaceholder.typicode.com/todos');
    const data = await response.json();
    tasks.value = data.map((task) => task.title);
  } catch (error) {
    console.log('Error fetching tasks');
  }
});
</script>
<template>
  <h1>{{ name }}</h1>
  <p v-if="status === 'active'">User is active</p>
  <p v-else="status === 'pending'">User is inactive</p>

  <form @submit.prevent="addTask">
    <label for="newTask">Add Task</label>
    <input type="text" id="newTask" v-model="newTask" />
    <button type="submit">Add</button>
  </form>
  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task, index) in tasks" :key="task">
      <span>{{ task }}</span>
      <button @click="deleteTask(index)">x</button>
    </li>
  </ul>
  <!-- <a :href="link">Google</a> -->
  <br />
  <button @click="toggleStatus">Change Status</button>
</template>
