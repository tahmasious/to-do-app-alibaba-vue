<script setup>
import ListItem from './components/listItem.vue';
import inputTask from './components/inputTask.vue';
import { ref } from 'vue';
let id = 1;
let tasks = ref(JSON.parse(localStorage.getItem("tasks")) == null ? [] : JSON.parse(localStorage.getItem("tasks")) );
console.log()
function updateLocalStorage(){
  localStorage.clear();
  localStorage.setItem("tasks", JSON.stringify(tasks.value));
}

function pushTask(content) {
  tasks.value.push({id : ++id, content : content, isDone: ref(false)});
  updateLocalStorage()
}

function deleteTask(i) {
  tasks.value.splice(i, 1);
  updateLocalStorage();
}

</script>

<template>
  <div class="bg-[#111111] min-h-screen"> 
    <div class="max-w-5xl m-auto p-3">
      <inputTask @add-task="(content) => pushTask(content)" />
      <div class="flex justify-start gap-1 flex-wrap">
        <div v-for="(task, index) in tasks" :key="task.id" >
          <ListItem @delete-item="deleteTask(index)" @markAsDone="() => {task.isDone = !task.isDone; updateLocalStorage()}" :isDone="task.isDone" >{{ task.content }}</ListItem>
        </div>
      </div>
    </div>
  </div>
</template>


