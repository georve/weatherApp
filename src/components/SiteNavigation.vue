<template>
    <header class="sticky top-o bg-weather-primary shadow-lg">
      <nav class="container flex flex-col sm:flex-row items-center gap-4 text-white py-6">
        <RouterLink :to="{name:'home'}">
            <div class="flex items-center gap-3">
                <i class="fa-solid fa-sun text-2xl"></i>
                <p class="text-2xl">The Local Weather</p>
            </div>
        </RouterLink>
        <div class="flex gap-3 flex-1 justify-end">
             <i class="fa-solid fa-circle-info text-xl 
              hover:text-weather-secondary duration-150" 
              @click = "toggleModal"></i>
              <i class="fa-solid fa-plus text-xl
               hover:text-weather-secondary duration-150 cursor-pointer"></i>
        </div>

        <BaseModal :modalActive="modalActive"
        @close-modal="toggleModal">
        <div class="text-black">
          <h1 class="text-2xl mb-1">About:</h1>
          <p class="mn-4">
           The local Weather allows you to track the current and future Weather of the cities of yoir choosing/
          </p>
          <h2 class="ext-2xl">How it works:</h2>
          <ol class="list-decimal list-inside mb-4">
            <li>
              Search for your citu by enterung the name into the searh bar
            </li>
            <li>
              tip2
            </li>
            <li>
              tip3
            </li>
          </ol>

          <h2 class="ext-2xl">Removing a city</h2>
          <ol class="list-decimal list-inside mb-4">
            <li>
              Search for your citu by enterung the name into the searh bar
            </li>
            <li>
              tip2
            </li>
            <li>
              tip3
            </li>

          </ol>
        </div>
        </BaseModal>
      </nav>
    </header>
</template>

<script setup>
import {ref} from "vue";
import {RouterLink} from "vue-router";
import BaseModal from "./BaseModal.vue"

const modalActive = ref(null);
const toggleModal = () => {
  modalActive.value=!modalActive.value;
}
</script>
