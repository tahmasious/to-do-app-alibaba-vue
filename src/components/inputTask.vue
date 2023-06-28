<template>
    <div>
        <form action="#" @submit.prevent="submitHandler" class="py-7">
            <input type="text" class="h-8 w-72 mr-3 rounded-2xl p-1" v-model="TaskValue">
            <button type="submit" class=" bg-slate-400  p-1 rounded-xl">Add task</button>
        </form>
    </div>
</template>

<script setup>
import { ref } from "vue";
const emit = defineEmits('addTask');
let TaskValue = ref('');
function submitHandler(){
    emit('addTask', TaskValue.value);
    TaskValue.value = '';
}
</script>


