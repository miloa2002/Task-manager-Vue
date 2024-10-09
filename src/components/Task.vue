<script setup>
import { computed } from 'vue';

defineEmits(["delete-task", "updated-task"])

const props = defineProps({
    task: {
        type: Object,
        required: true
    }
})

const changeCategory = computed(() => {
   if(props.task.category === "personal") {
    return "bg-orange-400 text-orange-900"
   }
   else if(props.task.category === "casa") {
    return "bg-green-400 text-green-900"
   }else if(props.task.category === "empresa") {
    return "bg-purple-400 text-purple-900"
   }
})

</script>

<template>
   <div class="bg-white shadow-md p-4 rounded-lg mt-11">
    <div class="flex items-center justify-between">
        <div :class="changeCategory" class="rounded-full px-3 py-2">
            {{ task.category }}
        </div>
        <div class="flex items-center gap-3">
            <img @click="$emit('updated-task', task.id)" class="cursor-pointer" src="../assets/edit-icon.png" alt="">
            <img @click="$emit('delete-task', task.id)" class="cursor-pointer" src="../assets/delete-icon.png" alt="">

        </div>
    </div>
    <div class="mt-4">
        <h3 class="text-xl font-bold mb-3">{{ task.title }}</h3>
        <p>{{ task.description }}</p>
    </div>

    <div class="flex justify-end text-slate-500 mt-10">
        <span>{{ task.date }}</span>
    </div>

   </div>
   
</template>
