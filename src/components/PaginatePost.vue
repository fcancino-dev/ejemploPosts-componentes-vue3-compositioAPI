<script setup>

    defineProps(["inicio", "fin", "maxlength"]);
    const emit = defineEmits(["next", "prev", "ini", "fin"]);

</script>

<template>
    <div class="inline-flex">
        <button 
            @click="emit('prev')"
            :disabled="inicio === 0"
            :class="{'bg-gray-50 hover:bg-gray-50 text-gray-300 font-bold py-2 px-4 rounded-l cursor-not-allowed': inicio === 0}"
            class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-l">
            Prev
        </button>
        <button 
            @click="emit('next')" 
            :disabled="fin >= maxlength" 
            :class="{'bg-gray-50 hover:bg-gray-50 text-gray-300 font-bold py-2 px-4 rounded-r cursor-not-allowed': fin >= maxlength}"
            class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-r">
            Next 
        </button>
        <button 
            @click="emit('ini')"
            class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-r">
            Start
        </button>
        <button 
            @click="emit('fn')"
            class="bg-gray-300 hover:bg-gray-400 text-gray-800 font-bold py-2 px-4 rounded-r">
            End
        </button>
    </div>
</template>