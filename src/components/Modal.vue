<script setup>

defineEmits(["delete-modal"])

defineProps({
    modal: {
        type: Boolean
    }
})

</script>

<template>
    <div v-if="modal" class="fixed inset-0 bg-black bg-opacity-50 flex justify-center items-center">
        <form class="bg-white w-1/4 h-auto p-4 rounded-md">
            <div class="flex justify-between items-center mb-4">
                <legend class="font-bold text-xl">Añadir nota</legend>
                <p @click="$emit('delete-modal')" class="text-2xl cursor-pointer">&times;</p>
            </div>

            <div class="flex items-center gap-4">
                <div class="w-1/2">
                    <label for="title" class="font-bold mb-2 block">Titulo</label>
                    <input class="outline-cyan-500 bg-gray-100 w-full p-2 rounded-md" type="text" id="title"
                        placeholder="Titulo de la tarea">
                </div>
                <div class="w-1/2">
                    <label for="title" class="font-bold mb-2 block">Categoría</label>
                    <select class="outline-cyan-500 bg-gray-100 w-full p-2 rounded-md" name="title" id="title">
                        <option value="">--Categoría--</option>
                        <option value="personal">Personal</option>
                        <option value="casa">Casa</option>
                        <option value="empresa">Empresa</option>
                    </select>
                </div>
            </div>

            <div class="w-full mt-4">
                <label for="description" class="font-bold mb-2 block">Descripción</label>
                <textarea placeholder="Descripción de la tarea" name="description" id="description" class="h-24 outline-cyan-500 bg-gray-100 w-full p-2 rounded-md"></textarea>
            </div>

            <div class="flex justify-end mt-6 gap-5">
                <button class="text-gray-400 font-bold" @click="$emit('delete-modal')">Cancel</button>
                <button class="text-white bg-cyan-500 p-2 rounded-full font-bold">Añadir</button>
            </div>
        </form>
    </div>
</template>