<script setup>
import { ref, computed } from 'vue';


const tasks = ref([
  { text: 'task 1', completed: false},
  { text: 'task 2', completed: false},
  { text: 'task 3', completed: true},
  { text: 'task 4', completed: true},
  { text: 'task 5', completed: true}
]);

const newTask = ref('')

const addTask = () => {
  if(newTask.value !== ''){
    tasks.value.push({
      text: newTask.value,
      completed: false
    })
  }
}

const completeTask = (task) => {
    task.completed = !task.completed   
}


const showCompleted = ref(false)
const fliterTasks = computed(() => {
  if(showCompleted.value) {
    return tasks.value
  } else {
    return tasks.value.filter(task => task.completed )
  }
})



</script>

<template>
  <div>

    <h1>Task list:</h1>
    <label for="completed"> completed </label>
    <input type="checkBox" v-model="showCompleted.value" name="completed">
  </div>

  <div>
    <ul>
      <li v-for="task in fliterTasks" :key="task.text">
        {{ task.text }}   {{ task.completed }}  
       <button @click="completeTask(task) ">Complete</button>
  
    </li>
  </ul>

  </div>

<h2>Add new task</h2>

<div>
  
  <input type="text" v-model="newTask">
  <button @click="addTask"> add Task</button>
</div>

  
</template>

<style scoped>
header {
  line-height: 1.5;
}

.taskComleted{
  text-decoration: line-through;
}

.logo {
  display: block;
  margin: 0 auto 2rem;
}

@media (min-width: 1024px) {
  header {
    display: flex;
    place-items: center;
    padding-right: calc(var(--section-gap) / 2);
  }

  .logo {
    margin: 0 2rem 0 0;
  }

  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }
}
</style>
