<script setup>
import { ref,onMounted} from 'vue'

    const name=ref('Sharal chalse');
    const status=ref('Inactive');
    const tasks=ref(['task1', 'task2', 'task3']);
    const newtask=ref('');
    const toggleStatus=()=>{
      if(status.value==='active'){
        status.value='inactive'
      } else {
        status.value='active'
      }
    };
    const addTask=()=>{
     if (newtask.value.trim()!==''){
      tasks.value.push(newtask.value);
      newtask.value='';
     }
    };
     const deleteTasks=(index)=>{
      tasks.value.splice(index,1);
      //index,1 means remove 1 element from the array at the specified index
    }
    onMounted(async()=>{
      try{
        const reponse=await fetch('https://jsonplaceholder.typicode.com/todos');
        const data=await reponse.json();
        tasks.value=data.map((task)=>task.title);
      }catch(error){
        console.log(error);
      }
    })
  
</script>

<template>
  <form @submit.prevent="addTask">
    <label for="new task">Add task</label>
    <input type="text" id="new task" v-model="newtask">
    <button type="submit">Submit</button>
  </form>
  <h3>hello Im {{ name }}</h3>
  <p v-if="status==='active'">User is active</p>
  <p v-else-if="status==='pending'">User is Pending</p>
  <p v-else>User is Inactive</p>
  <h3>Tasks:</h3>
  <ul>
    <li v-for="(task,index) in tasks" :key="task">
       <span>{{ task }}</span>
       <button @click="deleteTasks(index)">Delete</button>
      </li>
  </ul>
  <!-- <a :href="link">Click here for Google</a> -->
  <!-- <button v-on:click="toggleStatus">Change status</button> -->
  <button @click="toggleStatus">Change status</button>
 
</template>


