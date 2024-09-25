<script setup>
import { ref } from "vue";
import searchTaskVue from "./components/SearchTask.vue"

const categories = ref(['ALL','PERSONAL','HOME','BUSINESS'])

import searchTaskVue from "./components/searchTask.vue";
import Modal from "./components/Modal.vue"

const modal = ref(false)

const showModal = () => {
  modal.value = true;
}

const deleteModal = () => {
  modal.value = false;
}

</script>

<template>

  <main class= " h-screen w-full bg-gray-200">
    <searchTaskVue />


    <div class="container mx-auto">
      <h2 class="font-bold text-2xl mt-3">Your Notes</h2>

      <div>

        <div>
          <ul class="flex gap-2  text-sm font-medium border-b-2 max-w-min border-slate-600  ">
            <li 
            v-for="(item, index) in categories" 
            :key="index"
            
            class=" cursor-pointer">{{ item }}</li>
           
          </ul>

        </div>

        <div>

        </div>

      </div>

    </div>
    
    <searchTaskVue @show-modal="showModal" />
  </main>
  <Modal :modal="modal" @delete-modal="deleteModal" />
</template>