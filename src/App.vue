<script setup>
import ListItem from './components/listItem.vue';
import inputTask from './components/inputTask.vue';
import { computed, ref } from 'vue';
let id = 1;
let tasks = ref(JSON.parse(localStorage.getItem("tasks")) == null ? [] : JSON.parse(localStorage.getItem("tasks")) );
console.log()
function updateLocalStorage(){
  localStorage.clear();
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
}

function pushTask(content) {
  tasks.value.push({id : ++id, content : content, isDone: false});
  updateLocalStorage()
}

function deleteTask(i) {
  tasks.value.splice(i, 1);
  updateLocalStorage();
}

function markcomplete(index){
  tasks.value[index].isDone = !tasks.value[index].isDone; 
  updateLocalStorage()
}

const activeTasks = computed(() => tasks.value.filter((task) => !task.isDone).length)
</script>

<template>
  <div class="bg-[#111111] min-h-screen"> 
    <div class="max-w-5xl m-auto p-3">
      <inputTask @add-task="(content) => pushTask(content)" />
      
        <template v-if="tasks.length != 0">
          <div class="flex justify-start gap-1 flex-wrap">
              <div  v-for="(task, index) in tasks" :key="task.id" >
                <ListItem @delete-item="deleteTask(index)" @markAsDone="markcomplete(index)" :task="task" >{{ task.content }}</ListItem>
              </div>
            <hr>
            <br>
          </div>  
          <div class="text-white mt-3">
            <p v-if="activeTasks != 0"> {{ activeTasks }} active tasks</p>
            <p v-else>Nothing to do !</p>
          </div>
        </template>
        <div v-else>
          <p class="text-white">Add your first Task !</p>
        </div>
        
    </div>
  </div>
</template>


