<template>
    <div class="h-48 w-48 bg-[#737373] p-5 text-white rounded-xl flex flex-col justify-between">
        <p><slot></slot></p>
        <div class="flex justify-between">
            <button>
                <img src="../assets/check.svg" alt="check" class="h-5 w-5">
            </button>
            <button @click="$emit('deleteItem')">
                <img src="../assets/x.png" alt="remove" class="h-5 w-5">
            </button>
        </div>
    </div>
</template>


<script setup>
import { ref } from "vue";
defineEmits(['deleteItem']);
let isDone = ref(false);
</script>