<script setup>
import { onMounted, ref, watch } from "vue";
import searchTask from "./components/SearchTask.vue"
import Task from "./components/Task.vue";
import Modal from "./components/Modal.vue"
import { uid } from "uid";
import { reactive } from 'vue';
import moment from "moment";


const categories = ref(['ALL', 'PERSONAL', 'HOME', 'BUSINESS'])

const modal = ref(false)
const tasks = ref([])

const task = reactive({
  id: null,
  title: "",
  description: "",
  category: "",
  date: moment().format("DD/MM/YYYY")
})

watch(tasks, ()=>{
  guardarLocalStorage()
},{
  deep:true
})

const guardarLocalStorage = () => {
  localStorage.setItem('tasks', JSON.stringify(tasks.value))
}

onMounted(() => {

  const tasksStorage = localStorage.getItem('tasks')
  if (tasksStorage) {
    tasks.value = JSON.parse(tasksStorage)
    
  } 
   
})


const showModal = () => {
  modal.value = true;
}

const deleteModal = () => {
  modal.value = false;
}

const selectedCategory = ref("ALL")
const filteredTasks = ref([])

const selectMenu = (item) => {
  return selectedCategory.value = item
}

const addTask = () => {
  const {id} = task
  if(id) {
    const position = tasks.value.findIndex((task) => task.id === id)
    tasks.value[position] = {...task}
  }else{
    tasks.value.push({ ...task, id: uid() })
    guardarLocalStorage()
    
  }

  Object.assign(task, {
    id: null,
    title: "",
    description: "",
    category: "",
    date: moment().format("DD/MM/YYYY")
  })
}

const deleteTask = (id) => {
  tasks.value = tasks.value.filter(task => task.id !== id)
}

const updatedTask = (id) => {
  const taskFilter = tasks.value.filter(task => task.id === id)[0]

  Object.assign(task, taskFilter)
  showModal()
}

const searchTaskValue = (text) => {
  tasks.value.filter(t => t.title.includes(text.title))
}

</script>

<template>
  <main class=" h-screen w-full bg-gray-200">
    <searchTask :task="task" @search-task-value="searchTaskValue" @show-modal="showModal" />
    <div class="container mx-auto">
      <h2 class="font-bold text-2xl mt-3">Your Notes</h2>
      <div>
        <div>
          <ul class="flex gap-2  text-sm font-medium border-b-2 max-w-min border-slate-600  ">
            <li v-for="(item, index) in categories" :key="index" class="cursor-pointer" @click="selectMenu(item)"
              :class="[selectedCategory === item ? 'text-cyan-600' : 'text-gray-400']">{{ item }}</li>
          </ul>
        </div>
        <div>
        </div>
      </div>
    </div>
    <div class="container mx-auto">
      <div class="grid grid-cols-3 items-center gap-4">
        <Task @updated-task="updatedTask" @delete-task="deleteTask" v-for="task in tasks" :key="task.id" :task="task" />
      </div>
    </div>
  </main>
  <Modal :task="task" @add-task="addTask" :modal="modal" @delete-modal="deleteModal" v-model:title="task.title"
    v-model:description="task.description" v-model:category="task.category" :id="task.id" :date="task.date" />
</template>