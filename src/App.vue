<script setup>
import { ref } from "vue";
import searchTaskVue from "./components/SearchTask.vue"



const categories = ref(['ALL','PERSONAL','HOME','BUSINESS'])



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
    

    

  </main>
 
</template>