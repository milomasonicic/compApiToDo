<script setup>
       import { ref, reactive, computed } from 'vue'
     
       const state = reactive({ count1: 0 })
     
       const proxyTasks = reactive([
         { text: 'task1', complete: false},
         { text: 'task2', complete: true},
       ])
     
       const newTask = ref('') 
     
       const addTask = () => {
         if( newTask !== ''){
           proxyTasks.push({
             text: newTask.value, 
             complete: false
           })
         }
       }

       const completeFunction = (task) => {
        task.complete = !task.complete
       }
     
       const deleteFunction = (task) => {
        const taskId = proxyTasks.indexOf(task)
        if(taskId !== -1){
          proxyTasks.splice(taskId, 1)
        }
       }

       //true 
       const computedTaskTrue = computed(() => {
         return proxyTasks.filter(task => task.complete)
       })

       //false
       const computedTaskFalse = computed(() => {
         return proxyTasks.filter(task => !task.complete)
       })
     
</script>
<template>
      
   <ul>
    <li v-for="task in proxyTasks" :key="task.index">
      {{ task.text }} {{ task.complete }} 
       <button @click= "completeFunction(task)"> Complete</button>
       <button @click= "deleteFunction(task)"> Delete</button>

   </li>
      
    </ul>
      
    <input type="text" v-model="newTask">
    <button @click="addTask"> Add</button>
      
   <h1>	Counter </h1>
    <button @click="state.count1++">
     {{ state.count1 }}
     </button>
      
      <div>
        <h1>Urađeni taskovi</h1>
        <ul v-for="trueTask in computedTaskTrue" :key="trueTask.index">
          <li>
             
            {{trueTask.text}}
          </li>
        </ul>
      </div>

      <div>
        <h1>False taskovi</h1>
        <ul v-for="falseTask in computedTaskFalse" :key="falseTask.index">
          <li>
            {{falseTask.text}}
          </li>
        </ul>
      </div>
</template>


