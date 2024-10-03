<script setup>
import Task from './Task.vue';


const emit = defineEmits(["delete-modal", "add-task", "update:title", "update:description", "update:category"])


const prospTask = defineProps({
    modal: {
        type: Boolean
    },
    title: {
        type: String,
        required: true
    },
    description: {
        type: String,
        required: true
    },
    category: {
        type: String,
        required: true
    },
    id: {
        type: [String, null],
        required: true
    },
    date: {
        type: String,
        required: true
    },
})


const validateForm = () => {
    if (Object.values(prospTask).includes("")) {
        alert("Los campos no pueden ir vacíos");
        return
    }

    emit("add-task")
    emit("deleteModal")
}

</script>

<template>
    <div v-if="modal" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center">
        <form @submit.prevent="validateForm" class="bg-white w-1/4 h-auto p-4 rounded-md">
            <div class="flex justify-between items-center mb-4">
                <legend class="font-bold text-xl">{{id ? "Editar nota" : "Añadir nota" }}</legend>
                <p @click="$emit('delete-modal')" class="text-2xl cursor-pointer">&times;</p>
            </div>

            <div class="md:flex items-center gap-4">
                <div class="md:w-1/2">
                    <label for="title" class="font-bold mb-2 block">Titulo</label>
                    <input @input="$emit('update:title', $event.target.value)" :value="title" class="outline-cyan-500 bg-gray-100 w-full p-2 rounded-md" type="text"
                        id="title" placeholder="Titulo de la tarea">
                </div>
                <div class="md:w-1/2">
                    <label for="title" class="font-bold mb-2 block">Categoría</label>
                    <select @input="$emit('update:category', $event.target.value)" :value="category" class="outline-cyan-500 bg-gray-100 w-full p-2 rounded-md"
                        name="title" id="title">
                        <option value="">--Categoría--</option>
                        <option value="personal">Personal</option>
                        <option value="casa">Casa</option>
                        <option value="empresa">Empresa</option>
                    </select>
                </div>
            </div>

            <div class="w-full mt-4">
                <label for="description" class="font-bold mb-2 block">Descripción</label>
                <textarea @input="$emit('update:description', $event.target.value)" :value="description" placeholder="Descripción de la tarea" name="description"
                    id="description" class="h-24 outline-cyan-500 bg-gray-100 w-full p-2 rounded-md"></textarea>
            </div>

            <div class="flex justify-end mt-6 gap-5">
                <button class="text-gray-400 font-bold" @click="$emit('delete-modal')">Cancel</button>
                <button class="text-white bg-cyan-500 p-2 rounded-full font-bold">{{id ? "Editar tarea" : "Añadir tarea" }}</button>
            </div>
        </form>
    </div>
</template>