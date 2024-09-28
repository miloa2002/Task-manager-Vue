<script setup>
import { ref } from "vue";
import searchTask from "./components/SearchTask.vue"
import Modal from "./components/Modal.vue"

const categories = ref(['ALL', 'PERSONAL', 'HOME', 'BUSINESS'])

const modal = ref(false)

const showModal = () => {
  modal.value = true;
}

const deleteModal = () => {
  modal.value = false;
}

const selectedCategory = ref("ALL")

const selectMenu = (item) => {
  return selectedCategory.value = item
}
</script>

<template>
  <main class=" h-screen w-full bg-gray-200">
    <searchTask @show-modal="showModal" />
    <div class="container mx-auto">
      <h2 class="font-bold text-2xl mt-3">Your Notes</h2>
      <div>
        <div>
          <ul class="flex gap-2  text-sm font-medium border-b-2 max-w-min border-slate-600  ">
            <li 
              v-for="(item, index) in categories" 
              :key="index" class="cursor-pointer"
              @click="selectMenu(item)"
              :class="[selectedCategory === item ? 'text-cyan-600' : 'text-gray-400']"
            >{{ item }}</li>
          </ul>
        </div>
        <div>
        </div>
      </div>
    </div>
  </main>
  <Modal :modal="modal" @delete-modal="deleteModal" />
</template>