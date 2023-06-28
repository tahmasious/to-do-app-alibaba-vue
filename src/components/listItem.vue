<template>
    <div :class="{done : task.isDone}" class="h-48 w-48 bg-[#737373] p-5 text-white rounded-xl flex flex-col justify-between">
        <p>{{ task.content }}</p>
        <div class="flex justify-between">
            <button @click="$emit('markAsDone')">
                <img v-if="!task.isDone" src="../assets/check.svg" alt="check" class="h-5 w-5">
                <img v-else src="../assets/redo.png" alt="check" class="h-5 w-5">
            </button>
            <button @click="$emit('deleteItem')">
                <img src="../assets/x.png" alt="remove" class="h-5 w-5">
            </button>
        </div>
    </div>
</template>


<script setup>
defineEmits(['deleteItem', 'markAsDone']);
const props = defineProps(['task']);
console.log(props.task)
</script>

<style scoped>
.done {
    background-color: #1DB954!important;
}
</style>