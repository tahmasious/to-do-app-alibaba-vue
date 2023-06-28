<template>
    <div :class="{done : taskState}" class="h-48 w-48 bg-[#737373] p-5 text-white rounded-xl flex flex-col justify-between">
        <p><slot></slot></p>
        <div class="flex justify-between">
            <button @click="() => {$emit('markAsDone'); taskState = !taskState}">
                <img v-if="!taskState" src="../assets/check.svg" alt="check" class="h-5 w-5">
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
const props = defineProps(['isDone']);
let taskState = props.isDone;
</script>

<style scoped>
.done {
    background-color: #1DB954!important;
}
</style>