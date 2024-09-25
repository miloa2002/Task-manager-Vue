<script setup>
import { ref } from "vue";
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
    <searchTaskVue @show-modal="showModal" />
  </main>
  <Modal :modal="modal" @delete-modal="deleteModal" />
</template>