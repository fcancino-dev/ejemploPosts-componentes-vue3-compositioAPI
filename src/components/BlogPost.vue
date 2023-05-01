<script setup>
// defineProps(["title", "id", "body", "colortext"]);   // primera manera de escribirlo

// segunda manera de escribirlo
defineProps({
  title: String,
  id: Number,
  body: {
    type: String,
    default: "Sin descripcion",
  },
  //   cambiarfavorito: Function,
});

const emit = defineEmits(["cambiarfavorito", "eliminarfavorito"]);
</script>

<template>
    <div class="mt-2">
        <div
        class="border-r border-b border-l border-t border-gray-400 lg:border-l lg:border-t lg:border-gray-400 bg-white rounded-b rounded-l lg:rounded-b lg:rounded-r p-4 flex flex-col justify-between leading-normal"
        >
            <h1 class="text-gray-900 font-bold text-xl mb-2">{{ id }} - {{ title }}</h1>
            <p class="text-gray-700 text-base">{{ body }}</p>
            <div class="mt-2 flex space-x-4">
                <button
                    @click="emit('cambiarfavorito', title)"
                    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                >
                    Favorito
                </button>
                <button
                    @click="emit('eliminarfavorito')"
                    class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
                >
                    Eliminar de Favorito
                </button>
            </div>
        </div>
    </div>
</template>
