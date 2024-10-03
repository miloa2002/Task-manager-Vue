<script setup>
import { ref } from 'vue';

defineEmits(["show-modal", "search-task-value"])

const props = defineProps({
    task: {
        type: Object,
        required: true
    }
})

const searchText = ref("")


</script>

<template>
    <div class=" bg-white p-3 shadow-md">
        <div class="container mx-auto  flex items-center gap-4">
            <input @input="$emit('search-task-value', $event.target.value)" :value="searchText" placeholder="Buscar Tarea..." type="text" class=" w-full border-cyan-500 border outline-none rounded-md p-2 text-gray-500">
            <div class="cursor-pointer flex justify-center items-center gap-2 bg-cyan-400 p-2 text-white rounded-full" @click="$emit('show-modal')">
                <span>+</span>
                <button>Add</button>
            </div>
        </div>
    </div>
</template>
