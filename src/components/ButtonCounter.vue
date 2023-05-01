<script setup >
import { ref } from 'vue';

const counter = ref(0);
const increment = () => counter.value++;

</script>

<template>
    <button @click="increment" class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" >
    Counter: {{counter}}
    </button>
</template>